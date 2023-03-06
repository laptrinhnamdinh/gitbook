---
description: >-
  Redirect domain trong IIS dùng file web.config, redirect https to http, điều
  hướng tên miền từ http sang https
---

# Redirect domain trong IIS

```aspnet
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <httpRedirect enabled="true" destination="https://yourdomain/" />
    </system.webServer>
</configuration>
```
