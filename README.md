# httpclient

http wrapper with fault tolerance support

    import "github.com/lysu/httpclient"




## Constants
``` go
const (
    DefaultSuccessiveFailThreshold = 5
    DefaultTrippedBaseTime         = 20 * time.Millisecond
    DefaultTrippedTimeMax          = 100 * time.Millisecond
    DefaultRetryMaxServerPick      = 3
    DefaultRetryMaxRetryPerServer  = 0
    DefaultRetryBaseInterval       = 10 * time.Millisecond
    DefaultRetryMaxInterval        = 50 * time.Millisecond
)
```


## func ConstructQueryURL
``` go
func ConstructQueryURL(protocol, host, url string, params interface{}) (string, error)
```
ConstructQueryURL is used to construct query string and encode params


## func ConstructURL
``` go
func ConstructURL(protocol, host, url string) string
```
ConstructURL is used to construct url


## func WithBreaker
``` go
func WithBreaker(successiveFailThreshold uint, trippedBaseTime, trippedTimeMax time.Duration) func(o *httpConf)
```
WithBreak config http failure break params.


## func WithRetry
``` go
func WithRetry(retryMaxServerPick, retryMaxPerServer uint, retryBaseInterval, retryMaxInterval time.Duration) func(o *httpConf)
```
WithRetry config http retry params.



## type Client
``` go
type Client struct {
    Client       *http.Client
    LoadBalancer *slb.LoadBalancer
}
```
Client is used to send http request









### func NewHTTP
``` go
func NewHTTP(hosts []string, connTimeout, endToEndTimeout time.Duration, maxIdleConnsPerHost int, opts ...func(o *httpConf)) *Client
```
NewHTTP is used to create new http client


### func NewHTTPWithClient
``` go
func NewHTTPWithClient(client *http.Client, hosts []string, opts ...func(o *httpConf)) *Client
```
NewHTTPWithClient is used to create new client base on exists client for reuse connection pool.




### func (\*Client) Get
``` go
func (c *Client) Get(ctx context.Context, url string, handler HanldleResp) error
```
Get is used to invoke HTTP Get request



### func (\*Client) Post
``` go
func (c *Client) Post(ctx context.Context, url string, contentType string, body io.Reader, handler HanldleResp) error
```
Post is used to invoke HTTP Post request



### func (\*Client) PostForm
``` go
func (c *Client) PostForm(ctx context.Context, url string, data url.Values, handler HanldleResp) error
```
PostForm is used to invoke HTTP Post request in form content



### func (\*Client) Put
``` go
func (c *Client) Put(ctx context.Context, url string, contentType string, body io.Reader, handler HanldleResp) error
```
Put is used to invoke HTTP Put request



## type HanldleResp
``` go
type HanldleResp func(resp *http.Response) error
```
















- - -
Generated by [godoc2md](http://godoc.org/github.com/davecheney/godoc2md)
