

# LAYOUT

## HStack and VStack

# @ViewBuilder
> LISTS OF VIEWS
# PROTOCOL
> API? SIMILAR TO INTERFACE OF JAVA 
> SORT OF A "STRIPPED-DOWN" STRUCT/CLASS

A MUCH MORE COMMON USAGE IS TO SPECIFY THE BEHAVIOR OF A STRUCT, CLASS OR ENUM.
```
struct EmojiMemoryGameView: View
class EmojiMemoryGame: ObservableObject
```
# SHAPE
LECTURE 6
YOU WILL CREATE AND RETURN A Path THAT DRAWS ANYTHING YOU WANT.
# ViewModifier
THE ViewModifier PORTOCOL HAS ONE FUNCTION IN IT.

## ANIMATION
IMPORTANT TAKEWAWYS ABOUT ANIMATION
> ONLY CHANGES CAN BE ANIMATED. CHANGES TO:
> - ViewModifier arguments
> - Shapes
> - The "existence" (or not) of a View in the UI

ANIMATION IS SHOWING THE USER CHANGES THAT HAVE ALREADY HAPPENED( I.E. THE RECENT PAST).
ViewModifiers are the primary "change agents" in the UI.
### IMPLICIT ANIMATION
> **GOLDEN RULES**
THE ANIMATION ONLY ANIMATE CHANGES
WE CAN ONLY ANIMATE ViewModifiers FOR VIEWS THAT ARE ALREADY ON SCREEN
> see what it's like to diagnose the problem when an animation fails to fire   use  GOLDEN RULES
## ANIMATION DEMONSTRATION
LECTURE 8

# EmojiArt BRAND NEW DEMO


---


# Get rid of code bulk

```swift
   // or [String] UI portion is all

   **var** emojis = ["🚌", "🚝", "🚆", "🚇", "🛩", "🛶",
>
> ​         "🚟", "🚨", "🚁", "🚣", "🎠", "🏚",
>
> ​         "😶", "😬", "☺️", "🏠", "🏡", "🏘",
>
> ​         "🏢", "🏬", "🕍", "🕌", "⛪️", "🏛",
>
> ​         "💒", "🏫", "🏕", "🗻", "🌋", "🏜",]
>
>   // Left side of mutating operator isn't mutable: 'self' is immutable
>
>   // this should be a pointer to it
>
>   @State **var** emojiCount: Int = 20
>
>    

> ​    .onTapGesture{
>
> ​      isFaceUp = !isFaceUp
>
> ​    }

>   **var** content: String
>
>   // var must have initial value
>
>   @State **var** isFaceUp: Bool = **true**

> Spacer()
>
> ​      HStack{
>
> ​        remove
>
> ​        Spacer()
>
> ​        add
>
> ​        }
>
> ​      .font(.largeTitle)
>
> ​      .padding(.horizontal)

>   // use local varibles to clean up our code
>
>   **var** remove: **some** View{
>
> ​    // action emmm clean design
>
> ​    // you can del the (action: ) and the , before label
>
> ​    // 函数式预言的感觉 函数名后直接跟参数
>
> ​    // parameters follows the func name, this para is a 闭包
>
> ​    Button(action: {
>
> ​      **if** emojiCount > 1{
>
> ​        emojiCount -= 1
>
> ​      }
>
> ​    }, label: {
>
> ​      Image(systemName: "minus.circle")
>
> ​    })
>
>   }
>
>   **var** add: **some** View{
>
> ​    Button(action: {
>
> ​      **if** emojiCount < emojis.count{
>
> ​        emojiCount += 1
>
> ​      }
>
> ​    }, label: {
>
> ​      // Text("🏜")
>
> ​      // .font(.largeTitle)
>
> ​      Image(systemName: "plus.circle")
>
> ​    })
>
>   }