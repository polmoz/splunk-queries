# splunk queries and examples by polmoz

## 08-31-2024

### ** Daily Notes **
  - [x] Udemy course examples
  - [x] Youtube video examples

### ** SPL queries and examples **

- Example to visulize access invents from internal splunk index and use Bubble Chart visualization
```
index = _internal sourcetype=splunkd_access | stats count sum(bytes) as total_bytes by status, date_hour | table status date_hour count total_bytes status
```

- Example to convert search query to a table display
```
index=web 
| table clientip, action
```

- Example to calculate sum of bytes captured and format with specific, easy to read string
```
index=web OR index=security 
| stats sum(bytes) as Total_Bytes 
| eval Total_Bytes = tostring(Total_Bytes, "commas")
```

- Example to display top 6 categories and sum count
```
index=web action=purchase 
| top limit=6 categoryId 
| stats sum(count) as "Total Purchases Made"
```

- Example to display table with renamed columns and filtered records
```
index=web
| table clientip, action, categoryId, status
| where isnotnull(action)
| rename action as "ACTION", clientip as "Shoppers IP"
| fields - status
```

- Example to display table view with deduplicated (unique) records
```
index=web
| table clientip 
| dedup clientip
```

- Example to display sorted records with stats and count
```
index=web
| stats count by clientip 
| sort - count
```

- Example to display top values and not show percentage column
```
index=web | top limit=20 file showperc=f
```

- Example to display logging atempts from security logs, fill values where "null" (Note to also create colors for visualization specific to value ranges)
```
index=security
| stats values(user) as "Login Name", count(user) as "Attempts" by src
| fillnull value="no data available"
```

#### Tech Study notes and references:
  1. [ Splunk Search details and intro ] ([https://www.youtube.com/watch?v=IaA9YNlg5hM&t=303s](https://www.splunk.com/en_us/resources/videos/basic-search-in-splunk-enterprise.html))


## 09-01-2024

### ** Daily Notes **
  - [ ] Udemy course examples
  - [ ] Youtube video examples

### ** SPL queries and examples **

- Example to display eval command and time conversation and formatting
```
index=_internal
| eval epoch_time  = strptime(_time, "%s")
| eval human_readable_time = strftime(epoch_time, "%m/%d/%y %H:%M")
| table _time, epoch_time, human_readable_time
```

#### Tech Study notes and references:
  1. [ Splunk details and intro ]