# ⚙️ Setup

### Configuration

Tambahkan ke envronment service anda apabila anda ingin mengunakan collection core service, serta jangan lupa untuk menambahkan dalam file config anda

```

GRPC_ADDRESS="{ip_address:port_number}"
PROJECT_ID="{project_id}"
PROJECT_NAME="{project_name}"
CREDENTIAL_FILE="config/gcp_credential_account_service.json"
ROOT_COLLECTION_ID="{collection_id}"
ROOT_DOCUMENT_ID="{document_id}"
TOPIC="{topic_name}"

```

{% code lineNumbers="true" %}
```go
package <your_package>

type Config struct {
    GRPCAddress      string `json:"grpc_address" env:"GRPC_ADDRESS"`
    RootCollectionID string `json:"root_collection_id" env:"ROOT_COLLECTION_ID"`
    RootDocumentID   string `json:"root_document_id" env:"ROOT_DOCUMENT_ID"`
    ProjectID        string `json:"project_id" env:"PROJECT_ID"`
    ProjectName      string `json:"project_name" env:"PROJECT_NAME"`
    CredentialFile   string `json:"credential_file" env:"CREDENTIAL_FILE"`
    Topic            string `json:"topic" env:"TOPIC"`
}
```
{% endcode %}

{% hint style="info" %}
Hapus struct tags nya apabila tidak dibutuhkan
{% endhint %}

### Initiator SDK Client

Kamu dapat memanggil lagi client ini ke dalam package lain hanya dengan satu inisiasi.

initiator ini dibuat agar bisa digunakan berkali kali

<pre class="language-go" data-line-numbers><code class="lang-go"><strong>package &#x3C;your_package>
</strong><strong>
</strong><strong>import (
</strong>	"&#x3C;pkg>/&#x3C;internal>/config"
<strong>	"&#x3C;pkg-core>/collection_core"
</strong><strong>	"context"
</strong><strong>	"log"
</strong><strong>)
</strong><strong>
</strong><strong>func RegistryCollectionCoreClient(ctx context.Context, cfg *config.Config) collection_core.Client {
</strong>	var (
		client_opts = []collection_core.ConfigOption{
			collection_core.WithConfig_Firestore(cfg.RootCollectionID, cfg.RootDocumentID),
			collection_core.WithConfig_GRPC(cfg.GRPCAddress),
			// Pub/Sub Is Optional
			collection_core.WithConfig_PubSub(
				cfg.ProjectID,
				cfg.ProjectName,
				cfg.CredentialFile,
				cfg.Topic,
			),
		}
	)
	
	client, err := collection_core.NewClient(ctx, client_opts...)
	if err != nil {
		log.Println(err)
		return nil
	}
	
	return client
}
</code></pre>

{% hint style="info" %}
Jangan lupa untuk memangil `client.Close()` ketika server akan di matikan.
{% endhint %}

{% hint style="warning" %}
Handle panic harus diberikan apabila konfigurasi kosong!
{% endhint %}

### Implementasi

Dalam penggunaan SDK ini anda hanya perlu memasukan `collection_core.Client` pada field struct anda, contoh struct implementation:

{% hint style="warning" %}
Please use `defer query.Close()` after using query to help GO Garbage Collector clear a memory heap object.
{% endhint %}

```go
type ImpSomeStructure struct {
    client *collection_core.Client
}

func NewSomeStructure(client *collection_core.Client) *ImpSomeStructure {
    return &ImpSomeStructure{client: client}
}

type City struct {
    // this field to get document id
    CollectionCore_RefID string    `json:"collection_core_ref_id,omitempty"`
    
    // General Fields
    // when save this follow json tag
    // if json tag not set will follow field name
    Name                 string    `json:"name"`
    State                string    `json:"state"`
    Country              string    `json:"country"`
    Capital              bool      `json:"capital"`
    Population           int       `json:"population"`
    CreatedAt            time.Time `json:"created_at"`
    UpdatedAt            time.Time `json:"updated_at"`
}

type Order struct {
    By string
    Type string
}

type Filter struct {
    By string
    Op string
    Val interface{}
}

type Params struct {
    PerPage int
    Page int
    Filter []Filter
    Order []Order
}

func (imp *ImpSomeStructure) FindListCity(ctx context.Context, p *Params) ([]City, error) {
    var (
        query         = imp.client.NewQuery()
        cities        = make([]City, 0)
        query_cities  = query.Col("cities")
    )
    defer query.Close()
    
    for i := 0; i < len(p.Filter); i++ {
        f := p.Filter[i]
        query_cities.Where(f.By, f.Op, f.Val)
    }
    
    for i := 0; i < len(p.Order); i++ {
        var (
            o = p.Order[i]
            t collection_core.Direction
        )
        switch strings.ToUpper(f.Type) {
            case "ASC":
                t = collection_core.ASC
            case "DESC":
                t = collection_core.DESC
            default:
                continue
        }
        query_cities.OrderBy(o.By, t)
    }
    
    // Response Information Metadata:
    //
    // type ResponseInformation struct {
    //	    ReqID   xid.ID  `json:"req_id"`
    //	    Status  codes.Code `json:"status"`
    //	    Meta    Meta       `json:"meta"`
    //	    Message string     `json:"message"`
    // }
    //
    // type Meta struct {
    //	    Page    int32 `json:"page"`
    //	    PerPage int32 `json:"per_page"`
    //	    Size    int32 `json:"size"`
    // }
    //
    // This Support Pagination
    //  - Limit
    //  - Page
    response_info, err := query_cities.Limit(p.PerPage).Page(p.Page).Retrive(ctx, &cities)
    if err != nil {
        return nil, err
    }
    
    // https://pkg.go.dev/google.golang.org/grpc/codes
    if response_info.Status != codes.OK {
        return nil, errors.New(response_info.Message)
    }
    
    return cities, nil
}

func (imp *ImpSomeStructure) FindOneCity(ctx context.Context, state string) (*City, error) {
    var (
        query         = imp.client.NewQuery()
        city          = City{}
        query_city    = query.Col("cities")
    )
    defer query.Close()

    // Response Information Metadata:
    //
    // type ResponseInformation struct {
    //	    ReqID   xid.ID  `json:"req_id"`
    //	    Status  codes.Code `json:"status"`
    //	    Meta    Meta       `json:"meta"`
    //	    Message string     `json:"message"`
    // }
    //
    // type Meta struct {
    //	    Page    int32 `json:"page"`
    //	    PerPage int32 `json:"per_page"`
    //	    Size    int32 `json:"size"`
    // }
    response_info, err := query_city.Doc(state).Retrive(ctx, &cities)
    if err != nil {
        return nil, err
    }
    
    // https://pkg.go.dev/google.golang.org/grpc/codes
    if response_info.Status != codes.OK {
        return nil, errors.New(response_info.Message)
    }
    // Handle More by codes
    
    return &city, nil
}

func (imp *ImpSomeStructure) SaveCity(ctx context.Context, city *City, use_pubsub bool, merge_all bool) error {
    var (
        query = imp.client.NewQuery()
    )
    defer query.Close()

    // Response Information Metadata:
    //
    // type ResponseInformation struct {
    //	    ReqID   xid.ID     `json:"req_id"`
    //	    Status  codes.Code `json:"status"`
    //	    Meta    Meta       `json:"meta"`
    //	    Message string     `json:"message"`
    // }
    //
    // type Meta struct {
    //	    Page    int32 `json:"page"`
    //	    PerPage int32 `json:"per_page"`
    //	    Size    int32 `json:"size"`
    // }
    var opts = make([]SaveOption, 0)
    
    // Must Choose One
    if use_pubsub {
        // For Async Purpose 
        opts = append(opts, collection_core.IsUsePubSub)
    } else {
        // For Sync Purpose 
        opts = append(opts, collection_core.IsUseGRPC)
    }
    
    if merge_all {
        // https://cloud.google.com/firestore/docs/samples/firestore-data-set-doc-upsert#firestore_data_set_doc_upsert-go 
        opts = append(opts, collection_core.IsMergeAll)
    }
    
    // Set method has ability to create or update
    response_info, err := query.Col("cities").Doc(p.State).Set(ctx, city, opts...)
    if err != nil {
        return err
    }
    
    // https://pkg.go.dev/google.golang.org/grpc/codes
    if response_info.Status != codes.OK {
        return errors.New(response_info.Message)
    }
    // Handle More by codes
    
    return nil
}

func (imp *ImpSomeStructure) BulkSaveCity(ctx context.Context, cities []City, use_pubsub bool, merge_all bool) error {
    var (
        query = imp.client.NewQuery()
    )
    defer query.Close()

    // Response Information Metadata:
    //
    // type ResponseInformation struct {
    //	    ReqID   xid.ID     `json:"req_id"`
    //	    Status  codes.Code `json:"status"`
    //	    Meta    Meta       `json:"meta"`
    //	    Message string     `json:"message"`
    // }
    //
    // type Meta struct {
    //	    Page    int32 `json:"page"`
    //	    PerPage int32 `json:"per_page"`
    //	    Size    int32 `json:"size"`
    // }
    var opts = make([]SaveOption, 0)
    
    // Must Choose One
    if use_pubsub {
        // For Async Purpose 
        opts = append(opts, collection_core.IsUsePubSub)
    } else {
        // For Sync Purpose 
        opts = append(opts, collection_core.IsUseGRPC)
    }
    
    if merge_all {
        // https://cloud.google.com/firestore/docs/samples/firestore-data-set-doc-upsert#firestore_data_set_doc_upsert-go 
        opts = append(opts, collection_core.IsMergeAll)
    }
    
    // Set method has ability to create or update
    response_info, err := query.Col("cities").Set(ctx, cities, opts...)
    if err != nil {
        return err
    }
    
    // https://pkg.go.dev/google.golang.org/grpc/codes
    if response_info.Status != codes.OK {
        return errors.New(response_info.Message)
    }
    // Handle More by codes
    
    return nil
}
```
