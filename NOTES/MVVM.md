学习如何完成一个个单独的视图，再将一块块的代码组合成一个页面，最后再基础页面和交互的基础上使用`Model-View-ViewModel`的方式进行开发调整

> When working with fixed format dates, such as RFC 3339, you set the [`dateFormat`](https://developer.apple.com/documentation/foundation/dateformatter/1413514-dateformat) property to specify a format string. For most fixed formats, you should also set the [`locale`](https://developer.apple.com/documentation/foundation/dateformatter/1411973-locale) property to a POSIX locale (`"en_US_POSIX"`), and set the [`timeZone`](https://developer.apple.com/documentation/foundation/dateformatter/1411406-timezone) property to UTC.

```
let RFC3339DateFormatter = DateFormatter()
RFC3339DateFormatter.locale = Locale(identifier: "en_US_POSIX")RFC3339DateFormatter.dateFormat = "yyyy-MM-dd'T'HH:mm:ssZZZZZ"
RFC3339DateFormatter.timeZone = TimeZone(secondsFromGMT: 0) /* 39 minutes and 57 seconds after the 16th hour of December 19th, 1996 with an offset of -08:00 from UTC (Pacific Standard Time) */let string = "1996-12-19T16:39:57-08:00"
let date = RFC3339DateFormatter.date(from: string)
```

What does this Markdown file store? I don't recall the BMM stands for, damn.
