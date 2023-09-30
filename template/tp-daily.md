---
created: <% tp.date.now("YYYY-MM-DD HH:mm") %>
aliases: [<% tp.file.title %>]
weather: "<% tp.user.天氣_台北市() %>"
tags: [ daily ]
---
# <% tp.file.title %> 

Modified:: <%+ tp.file.last_modified_date() %>

← [[<% tp.date.yesterday("YYYY-MM-DD_ddd") %>]] | [[<% tp.date.tomorrow("YYYY-MM-DD_ddd")%>]] →

<!--% tp.web.random_picture("1600x900", tp.file.title) %-->

## 本日完成任務
```tasks
done today
```

## 未完成任務
```tasks
not done
due before today
```

## 未完成之無期限任務
```tasks
path does not include 000-Index
path does not include 010-Templates
path does not include todo
path does not include <% tp.file.title %>
not done
no due date
```

## 明天到期任務
```tasks
due on tomorrow
```
## 昨天完成任務
```tasks
done on yesterday
```

----

<%*
function getWeek() {
  var d = new Date();
  var n = d.getDay();
  return n;
}
let titleDate = tp.file.title;  // 可能在今天建立明天的日記，因此日期不能取系統日期
let index = titleDate.indexOf("_");
if (index > 0) {
  titleDate = titleDate.substring(0, index);
}

let week = getWeek();
if (week == 1 || week == 4) {
%>
## 會議

<%* } %>

## 任務

## 靈光一閃

## 每日檢核清單
### 一日之計在於晨
- [ ] 🔵檢查Email
- [ ] 🔵檢查即時通訊 (QQ)
- [ ] 🔵檢查即時通訊 (Discord)
- [ ] 🔵每日閱讀（Obsidian論壇，YouTube，ITHome，開源中國）
<%-*
if (week == 1) {
-%>
- [ ] 🔵周一閱讀（Obsidian Roundup）
<%* } %>
- [ ] 🔵檢查公告
- [ ] 🔵檢查待辦事項

### 今日事今日畢
- [ ] 🔵返家前檢查Email (@<% titleDate %> 18:05)
- [ ] 🔵返家前更新待辦事項狀態 (@<% titleDate %> 18:07)
- [ ] 🔵檢查明天待辦事項 (@<% titleDate %> 18:10)

### 明天到期任務
```tasks
due on tomorrow
```

## 其他事項


＃＃