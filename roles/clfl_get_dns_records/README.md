1) suppose, you're already have cloudflare account and your site DNS already added to Cloudflare.
2) Main Page->Websites->Overview, on the page:  
navigate bottom-right corner, section called `API`  
copy Zone ID `8d38956435a9cc1a64ceb73af4aa2fef`  
copy Account ID `c18cb55a69d74123e1df3f8a97cc7949`  

```
curl --request GET \
  --url https://api.cloudflare.com/client/v4/zones/$zone_id/dns_records \
  --header 'Content-Type: application/json' \
  --header "X-Auth-Key: $key"
  --header "X-Auth-Email: $email"
```

https://developers.cloudflare.com/api/operations/dns-records-for-a-zone-list-dns-records

#cloudflare