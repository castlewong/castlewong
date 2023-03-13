
is a way of ordering, placing files. Can be amended.

2022-10-18 11:14:20 

To add a border, use the Shape/stroke(:lineWidth:) modifier, and use the [inset(by:)](https://swiftontap.com/Circle/inset(by:)) modifier to inset the circle by half of the border width to keep the circle at its original size:



```swift
struct ExampleView: View {
    var body: some View {
        Circle()
            .inset(by: 10)
            .stroke(Color.blue, lineWidth: 20)
    }
}
```



2022-12-03 21:56:47
#problems
@main
Thread 1: "-[__NSTaggedDate intValue]: unrecognized selector sent to instance 0xa40c659893f07970"
