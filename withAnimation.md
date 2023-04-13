


## withAnimation

https://www.avanderlee.com/swiftui/withanimation-completion-callback/

## .animation()

> The `.animation()` modifier has been deprecated in iOS 15

I'm not sure I understand how Xcode's suggested equivalent, `animation(_:value:)`, works.

> ```swift
> .animation(.easeInOut(duration: 2)) // ⚠️'animation' was deprecated in iOS 15.0: Use withAnimation or animation(_:value:) instead.
> ```

How would I change my code to get rid of the warning?


You need tell Xcode what exactly should be animated! With given a variable that conform to Equatable protocol. That could be State or Binding or any other wrapper that allow you to update the value of it.

_**Example:**_

```swift
struct ContentView: View {
    
    @State private var offset: CGFloat = 200.0
    
    var body: some View {
        
        Image(systemName: "ant")
            .font(Font.system(size: 100.0))
            .offset(y: offset)
            .shadow(radius: 10.0)
            .onTapGesture { offset -= 100.0 }
            .animation(Animation.easeInOut(duration: 1.0), value: offset)
        
    }
}
```