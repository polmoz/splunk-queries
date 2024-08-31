# splunk queries and examples by polmoz

## 08-31-2024

### ** Daily Notes **
  - [x] Udemy course examples
  - [ ] Youtube video examples

### ** SPL queries and examples **
```
index = _internal sourcetype=splunkd_access | stats count sum(bytes) as total_bytes by status, date_hour | table status date_hour count total_bytes status
```
  
#### Tech Study notes and references:
  1. [ Splunk Search details and intro ] ([https://www.youtube.com/watch?v=IaA9YNlg5hM&t=303s](https://www.splunk.com/en_us/resources/videos/basic-search-in-splunk-enterprise.html))
