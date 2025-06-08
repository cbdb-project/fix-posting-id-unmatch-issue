# fix-posting-id-unmatch-issue

## Check 

```
SELECT 
    (SELECT MAX(c_posting_id) FROM POSTING_DATA) AS max_posting_data_id,
    (SELECT MAX(c_posting_id) FROM POSTED_TO_OFFICE_DATA) AS max_posted_to_office_id,
    (SELECT MAX(c_posting_id) FROM POSTED_TO_ADDR_DATA) AS max_posted_to_addr_id;
```

## Delete the unmatched data

```
DELETE FROM POSTING_DATA
WHERE c_posting_id = (SELECT MAX_ID FROM (SELECT MAX(c_posting_id) AS MAX_ID FROM POSTING_DATA) AS SUB);
```
