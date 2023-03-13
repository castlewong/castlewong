How can I use the GraphicalDatePicker without the time ?

```Swift
DatePicker("Enter your date", selection: $date, displayedComponents: .date)
.datePickerStyle(GraphicalDatePickerStyle())
```

add "displayedComponents: .date" to your [[DatePicker]]