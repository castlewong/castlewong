From [Apple🔗](https://developer.apple.com/tutorials/swiftui/animating-views-and-transitions)
SwiftUI in Action.

- [[#1. CREATING AND COMBINING VIEWS|1. CREATING AND COMBINING VIEWS]]
- [[#2. BUILDING LISTS AND NAVIGATION|2. BUILDING LISTS AND NAVIGATION]]
- [[#3. Handling User Input|3. Handling User Input]]
	- [[#3. Handling User Input#Question|Question]]
- [[#4. Drawing and Animation|4. Drawing and Animation]]
- [[#5. Drawing Paths and Shapes|5. Drawing Paths and Shapes]]
	- [[#5. Drawing Paths and Shapes#1. Create Drawing Data for a Badge View|1. Create Drawing Data for a Badge View]]
	- [[#5. Drawing Paths and Shapes#2. Draw the Badge Background|2. Draw the Badge Background]]
	- [[#5. Drawing Paths and Shapes#3. Draw the Badge Symbol|3. Draw the Badge Symbol]]
	- [[#5. Drawing Paths and Shapes#4. Combine the Badge Foreground and Background|4. Combine the Badge Foreground and Background]]
		- [[#4. Combine the Badge Foreground and Background#1. What is the purpose of `GeometryReader`?|1. What is the purpose of `GeometryReader`?]]
		- [[#4. Combine the Badge Foreground and Background#2. What shape does the following drawing code create?|2. What shape does the following drawing code create?]]
- [[#6. Animating Views and Transitions|6. Animating Views and Transitions]]
	- [[#6. Animating Views and Transitions#1. Add Hiking Data to the App|1. Add Hiking Data to the App]]
	- [[#6. Animating Views and Transitions#2. Add Animations to Individual Views|2. Add Animations to Individual Views]]
	- [[#6. Animating Views and Transitions#3. Animate the Effects of State Changes|3. Animate the Effects of State Changes]]
	- [[#6. Animating Views and Transitions#4. Customize View Transitions|4. Customize View Transitions]]
	- [[#6. Animating Views and Transitions#5. Compose Animations for Complex Effects|5. Compose Animations for Complex Effects]]
- [[#7. App Design and Layout|7. App Design and Layout]]
- [[#8. Composing Complex Interfaces|8. Composing Complex Interfaces]]
	- [[#8. Composing Complex Interfaces#1. Add a Category View|1. Add a Category View]]
	- [[#8. Composing Complex Interfaces#2. Create a Category List|2. Create a Category List]]
	- [[#8. Composing Complex Interfaces#3. Create a Category Row|3. Create a Category Row]]
	- [[#8. Composing Complex Interfaces#4. Complete the Category View|4. Complete the Category View]]
	- [[#8. Composing Complex Interfaces#5. Add Navigation Between Sections|5. Add Navigation Between Sections]]
- [[#9. Working with UI Controls|9. Working with UI Controls]]
	- [[#9. Working with UI Controls#1. Display a User Profile|1. Display a User Profile]]
	- [[#9. Working with UI Controls#2. Add an Edit Mode|2. Add an Edit Mode]]
	- [[#9. Working with UI Controls#3. Define the Profile Editor|3. Define the Profile Editor]]
	- [[#9. Working with UI Controls#4. Delay Edit Propagation|4. Delay Edit Propagation]]
- [[#10. Interfacing with UIKit|10. Interfacing with UIKit]]
	- [[#10. Interfacing with UIKit#1. Create a View to Represent a UIPageViewController|1. Create a View to Represent a UIPageViewController]]
	- [[#10. Interfacing with UIKit#2. Create the View Controller’s Data Source|2. Create the View Controller’s Data Source]]
	- [[#10. Interfacing with UIKit#3. Track the Page in a SwiftUI View’s State|3. Track the Page in a SwiftUI View’s State]]
	- [[#10. Interfacing with UIKit#4. Add a Custom Page Control|4. Add a Custom Page Control]]



How can I use the GraphicalDatePicker without the time ?

```
DatePicker("Enter your date", selection: $date, displayedComponents: .date)
.datePickerStyle(GraphicalDatePickerStyle())
```

add "displayedComponents: .date" to your DatePicker

## 1. CREATING AND COMBINING VIEWS

1. create a new project and explore the canvas

2. customize the text view

   > To customize a SwiftUI view you call methods called modifiers
   >
   > Modifiers wrap a view to change its display or other properties
   >
   > Each modifier returns a new views so it's commin to chain multiple modifiers stacked vertically

   Show SwiftUI Inspector

3. combine views using stacks

   > You can combine and embed multiple views in stacks which group views together 
   >
   > horizontally vertically or back-to-front
   >
   > By default, stacks center their contents along their axis and provide context-appropriate spacing.
   >
   > To direct the layout to use the full width of the device, separate the park and the state by adding a `Spacer` to the horizontal stack holding the two text views.
   >
   > > A *spacer* expands to make its containing view use all of the space of its parent view, instead of having its size defined only by its contents.
   >
   > 

4. create a custom image view

   > Add a call to `clipShape(Circle())` to apply the circular clipping shape to the image.
   >
   > The `Circle` type is a shape that you can use as a mask, or as a view by giving the circle a stroke or fill.

5. use SwiftUI views from other frameworks

   > Next you’ll create a map that centers on a given coordinate. You can use the `Map` view from MapKit to render the map.
   >
   > When you import SwiftUI and certain other frameworks in the same file, you gain access to SwiftUI-specific functionality provided by that framework.
   >
   > Create a private state variable that holds the region information for the map.
   >
   > > You use the `@State` attribute to establish a source of truth for data in your app that you can modify from more than one view. SwiftUI manages the underlying storage and automatically updates views that depend on the value.
   >
   > Replace the default `Text` view with a `Map` view that takes a binding to the region.
   >
   > > By prefixing a state variable with `$`, you pass a binding, which is like a reference to the underlying value. When the user interacts with the map, the map updates the region value to match the part of the map that’s currently visible in the user interface.

6. compose the detail view

   > To layer the image view on top of the map view, give the image an offset of -130 points vertically, and padding of -130 points from the bottom of the view.
   >
   > > These adjustments make room for the text by moving the image upwards.
   >
   > Add a spacer at the bottom of the outer `VStack` to push the content to the top of the screen.
   >
   > Finally, move the subheadline font modifier from each `Text` view to the `HStack` containing them, and apply the secondary color to the subheadline text.
   >
   > > When you apply a modifier to a layout view like a stack, SwiftUI applies the modifier to all the elements contained in the group.

   **Check your understanding**

   1. When creating a custom SwiftUI view, where do you declare the view’s layout?

   - In the view’s initializer.

     > Use the `body` property to declare the view’s layout.

   - In the `body` property.

     > Custom views implement the `body` property, which is a requirement of the `View` protocol.

   - In the `layoutSubviews()` method.

     > SwiftUI views are not `UIView` subclasses. Use the `body` property to declare the view’s layout.

   2. The nested horizontal and vertical stacks arrange the image to the left of the two text views.
   3. You can use a stack to return multiple views from a `body` property.
   4. Each modifier method returns a **new** view, so this code discards the results of the two modifier calls and returns the `Text` view unchanged. Modifiers are methods that you can call on views, not properties that you set. A modifier returns a view that applies a new behavior or visual change. You can **chain** multiple modifiers to achieve the effects you need.

## 2. BUILDING LISTS AND NAVIGATION

1. Create a Landmark Model

   In the first tutorial, you hard-coded information into all of your custom views.

   Here, you’ll create a model to store data that you can pass into your views.

   > Define a `Landmark` structure with a few properties matching names of some of the keys in the `landmarkData.json` data file.
   >
   > > Adding `Codable` conformance makes it easier to move data between the structure and a data file. You’ll rely on the `Decodable` component of the `Codable` protocol later in this section to read data from file.
   >
   > Add an `imageName` property to read the name of the image from the data, and a computed `image` property that loads an image from the asset catalog.
   >
   > > You make the property private because users of the `Landmarks` structure care only about the image itself.
   >
   > Add a `coordinates` property to the structure using a nested `Coordinates` type that reflects the storage in the JSON data structure.
   >
   > > You mark this property as private because you’ll use it only to create a public computed property in the next step.
   >
   > Step 9
   >
   > Create a `load(_:)` method that fetches JSON data with a given name from the app’s main bundle.
   >
   > > The load method relies on the return type’s conformance to the `Decodable` protocol, which is one component of the `Codable` protocol.
   >
   > group related files together to make it easier to manage your growing project.

2. Create the row view

   > When you add the `landmark` property, the preview stops working, because the `LandmarkRow` type needs a landmark instance during initialization.

3. Customize the row preview

   Xcode’s canvas automatically recognizes and displays any type in the current editor that conforms to the `PreviewProvider` protocol. A preview provider returns one or more views, with options to configure the size and device.

   You can customize the returned content from a preview provider to render exactly the previews that are most helpful to you.

   > Use the `previewLayout(_:)` modifier to set a size that approximates a row in a list.
   >
   > The code you write in a preview provider only changes what Xcode displays in the canvas.

4. create the list of Landmarks

   > provide `LandmarkRow` instances with the first two landmarks as the list’s children.

   > ```swift
   > List {
   >   LandmarkRow(landmark: landmarks[0])
   > 	LandmarkRow(landmark: landmarks[1])
   > }
   > ```

   > The preview shows the two landmarks rendered in a list style that’s appropriate for iOS.

5. make the list Dynamic

   > You can create a list that displays the elements of a collection by passing your collection of data and a closure that provides a view for each element in the collection. 
   >
   > The list transforms each element in the collection into a child view by using the supplied closure.

   > Lists work with *identifiable* data. You can make your data identifiable in one of two ways: 
   >
   > 1. by passing along with your data a key path to a property that uniquely identifies each element(below), or 
   > 2. by making your data type conform to the `Identifiable` protocol(down below).
   >
   > ```swift
   > struct LandmarkList: View {
   >     var body: some View {
   >         List(landmarks, id: \.id) { landmark in
   > 
   >         }
   >     }
   > }
   > 
   > import Foundation
   > import SwiftUI
   > import CoreLocation
   > 
   > struct Landmark: Hashable, Codable, Identifiable {
   >     var id: Int
   >     var name: String
   >     var park: String
   >     var state: String
   >     var description: String
   > 
   >     private var imageName: String
   >     var image: Image {
   >         Image(imageName)
   >     }
   > 
   >     private var coordinates: Coordinates
   >     var locationCoordinate: CLLocationCoordinate2D {
   >         CLLocationCoordinate2D(
   >             latitude: coordinates.latitude,
   >             longitude: coordinates.longitude)
   >     }
   > 
   >     struct Coordinates: Hashable, Codable {
   >         var latitude: Double
   >         var longitude: Double
   >     }
   > }
   > ```

6. set up navigation between list and detail

   The list renders properly, but you can’t tap an individual landmark to see that landmark’s detail page yet.

   **You add navigation capabilities to a list by embedding it in a `NavigationView`, and then nesting each row in a `NavigationLink` to set up a transtition to a destination view.**

   This is just **beautiful**

   ```swift
   NavigationView {
               List(landmarks) { landmark in
                   NavigationLink {
                       LandmarkDetail()
                   } label: {
                       LandmarkRow(landmark: landmark)
                   }
               }
               .navigationTitle("Landmarks")
           }
   ```

   A NAVIGATION VIEW CLICK YOU GO TO THE LandmarkDetail() and the .navigationTitle just trasform to a travel back title on the top left 

   **what a beautiful design**

7. Pass Data into Child Views

   The `LandmarkDetail` view still uses hard-coded details to show its landmark. Just like `LandmarkRow`, the `LandmarkDetail` type and the views it comprises need to use a `landmark` property as the source for their data.

   Starting with the child views, you’ll convert `CircleImage`, `MapView`, and then `LandmarkDetail` to display data that’s passed in, rather than hard-coding each row.

   > Even though you’ve fixed the preview logic, the preview fails to update because the build fails. The detail view, which instantiates a circle image, needs an input parameter as well.

   > Finally, call the `navigationTitle(_:)` modifier to give the navigation bar a title when showing the detail view, and the `navigationBarTitleDisplayMode(_:)` modifier to make the title appear inline.

   

8. Generate Previews Dynamically

   Next, you’ll add code to the `LandmarkList_Previews` preview provider to render previews of the list view at different device sizes. By default, previews render at the size of the device in the active scheme. You can change the preview device by calling the `previewDevice(_:)` modifier method.

   > Within the list preview, embed the `LandmarkList` in a `ForEach` instance, using an array of device names as the data.
   >
   > `ForEach` operates on collections the same way as the list, which means you can use it anywhere you can use a child view, such as in stacks, lists, groups, and more. When the elements of your data are simple value types — like the strings you’re using here — you can use `\.self` as key path to the identifier.
   >
   > ForEach is a puzzle. It is a type which presents a dynamic list of views from a collection
   >
   > **Qusetions**
   >
   > - In addition to `List`, which of these types presents a dynamic list of views from a collection?
   >
   > ```
   > Group
   > ```
   >
   > You can use groups and stacks to organize views and other content, but not directly from a collection without another type listed here.
   >
   > 
   >
   > ```
   > ForEach
   > ```
   >
   > Place a `ForEach` instance inside a `List` or other container type to create a dynamic list.
   >
   > 
   >
   > ```
   > UITableView
   > ```
   >
   > SwiftUI provides a new way to dynamically create lists in a cross-platform manner.
   >
   > 
   >
   > - You can create a `List` of views from a collection of `Identifiable` elements. What approach do you use to adapt a collection of elements that don’t conform to the `Identifiable` protocol?
   >
   >   
   >
   >   Calling `map(_:)` on the data.
   >
   >   The `map(_:)` method can convert the elements of a collection to a different type, but not necessarily one that conforms to the `Identifiable` protocol.
   >
   >   
   >
   >   Calling `sorted(by:)` on the data.
   >
   >   The `sorted(by:)` method is for sorting the data in your collection, not adapting it for `Identifiable` conformance.
   >
   >   
   >
   >   Passing a key path along with the data to `List(_:id:)`.
   >
   >   Pass the key path to a uniquely identifying property for your collection’s elements as the second parameter when creating a `List`.
   >
   >   
   >
   >   - Which type do you use to make rows of a `List` tappable to navigate to another view?
   >
   >   
   >
   >   ```
   >   NavigationLink
   >   ```
   >
   >   Provide the destination view and the content of a row when you declare a `NavigationLink`.
   >
   >   
   >
   >   ```
   >   UITableViewDelegate
   >   ```
   >
   >   A `UITableViewDelegate` responds to user interactiosn with a `UITableView`. SwiftUI provides a different type to add navigation to a list.
   >
   >   
   >
   >   ```
   >   NavigationView
   >   ```
   >
   >   `NavigationView` sets up a navigation hierarchy for a list and its children, but you need a different type to make rows act as buttons that navigate to another view.

## 3. Handling User Input

In the Landmarks app, a user can flag their favorite places, and filter the list to show just their favorites. 

To create this feature, you’ll start by adding a switch to the list so users can focus on just their favorites, and then you’ll add a star-shaped button that a user taps to flag a landmark as a favorite.

1. Mark the User’s Favorite Landmarks

   Begin by enhancing the list to show users their favorites at a glance. Add a property to the `Landmark` structure to read the initial state of a landmark as a favorite, and then add a star to each `LandmarkRow` that shows a favorite landmark.

   > The `landmarkData.json` file has a key with this name for each landmark. Because `Landmark` conforms to `Codable`, you can read the value associated with the key by creating a new property with the same name as the key in our **Model.**

   > In SwiftUI blocks, you use `if` statements to conditionally include views.

2. Filter the List View

   You can customize the list view so that it shows all of the landmarks, or just the user’s favorites. To do this, you’ll need to add a bit of *state* to the `LandmarkList` type.

   > *State* is a value, or a set of values, that can change over time, and that affects a view’s behavior, content, or layout. You use a property with the `@State` attribute to add state to a view.

   Step 2

   Add a `@State` property called `showFavoritesOnly` with its initial value set to `false`.

   Because you use state properties to hold information that’s specific to a view and its subviews, you always create state as `private`.

   When you make changes to your view’s structure, like adding or modifying a property, you need to manually refresh the canvas.

   > Compute a filtered version of the landmarks list by checking the `showFavoritesOnly` property and each `landmark.isFavorite` value.

3. Add a Control to Toggle the State

   To give the user control over the list’s filter, you need to add a control that can alter the value of `showFavoritesOnly`. You do this by passing a binding to a toggle control.

   A *binding* acts as a reference to a mutable state. When a user taps the toggle from off to on, and off again, the control uses the binding to update the view’s state accordingly.

   To combine static and dynamic views in a list, or to combine two or more different groups of dynamic views, use the `ForEach` type instead of passing your collection of data to `List`.

   You use the `$` prefix to access a binding to a state variable, or one of its properties.

4. Use an Observable Object for Storage

   To prepare for the user to control which particular landmarks are favorites, you’ll first store the landmark data in an *observable object.*

   An observable object is a custom object for your data that can be bound to a view from storage in SwiftUI’s environment. SwiftUI watches for any changes to observable objects that could affect a view, and displays the correct version of the view after a change.

   In ModelData 

   > Declare a new model type that conforms to the `ObservableObject` protocol from the Combine framework.

   > SwiftUI subscribes to your observable object, and updates any views that need refreshing when the data changes.

   > Declare a new model type that conforms to the `ObservableObject` protocol from the Combine framework.
   >
   > SwiftUI subscribes to your observable object, and updates any views that need refreshing when the data changes.
   >
   > > An observable object needs to publish any changes to its data, so that its subscribers can pick up the change. ⬇️
   >
   > Step 4
   >
   > Add the `@Published` attribute to the `landmarks` array.

   

   

5. Adopt the Model Object in Your Views

   Now that you’ve created the `ModelData` object, you need to update your views to adopt it as the data store for your app.

6. Create a Favorite Button for Each Landmark

   The Landmarks app can now switch between a filtered and unfiltered view of the landmarks, but the **list of favorite landmarks is still hard coded**. 

   To allow the user to add and remove favorites, you need to add a favorite button to the landmark detail view.

   Because you use a binding, changes made inside this view propagate back to the data source.

   

### Question

1. Which of the following passes data downward in the view hierarchy?

   

   The `@EnvironmentObject` attribute.

   You use this attribute in views that are lower down in the view hierarchy to receive data from views that are higher up.

   

   The `environmentObject(_:)` modifier.

   You apply this modifier so that views further down in the view hierarchy can read data objects passed down through the environment.

2. What’s the role of a binding?

   

   It’s a value and a way to change that value.

   A binding controls the storage for a value, so you can pass data around to different views that need to read or write it.

   It’s a way to link a pair of views together to ensure that they receive the same data.

   It’s a way to freeze a value temporarily so that other views don’t update during state transitions.

   Answer number 1 is correct

3. Which is the correct way to create state for a view?

   

   ```
   private var showFavoritesOnly: State = false
   ```

   Use the `@State` attribute at the beginning of the declaration to indicate that SwiftUI should manage the value as state.

   

   ```
   @State var showFavoritesOnly = false
   ```

   Always mark state properties as private because state should be specific to a view and its child views.

   

   ```
   @State private var showFavoritesOnly = false
   ```

   Use the `@State` property wrapper to mark a value as state, declare the property as private, and give it a default value.



## 4. Drawing and Animation

## 5. Drawing Paths and Shapes

Users receive a badge whenever they visit a landmark in their list. Of course, for a user to receive a badge, you’ll need to create one. This tutorial takes you through the process of creating a badge by combining paths and shapes, which you then overlay with another shape that represents the location.

If you want to create multiple badges for different kinds of landmarks, try experimenting with the overlaid symbol, varying the amount of repetition, or changing the various angles and scales.

### 1. Create Drawing Data for a Badge View

To create the badge, you’ll start by defining data that you can use to draw a hexagon shape for the badge’s background.

### 2. Draw the Badge Background

Use the graphics APIs in SwiftUI to draw a custom badge shape.

> You use paths to combine lines, curves, and other drawing primitives to form more complex shapes like the badge’s hexagonal background.
>
> Don’t worry if your hexagon looks a little unusual; that’s because you’re ignoring the curved part of each segment at the shape’s corners. You’ll account for that next.

### 3. Draw the Badge Symbol

The Landmarks badge has a custom insignia in its center that’s based on the mountain that appears in the Landmarks app icon.

The mountain symbol consists of two shapes: one that represents a snowcap at the peak, and the other that represents vegetation along the approach. You’ll draw them using two partially triangular shapes that are set apart by a small gap.

### 4. Combine the Badge Foreground and Background

The badge design calls for the mountain shape to be rotated and repeated multiple times on top of the badge background.

Define a new type for rotation and leverage the `ForEach` view to apply the same adjustments to multiple copies of the mountain shape.

#### 1. What is the purpose of `GeometryReader`?



You use `GeometryReader` to divide the parent view into a grid that you use to lay out views onscreen.

SwiftUI doesn’t use a grid-based layout system to position views.



You use `GeometryReader` to dynamically draw, position, and size views instead of hard-coding numbers that might not be correct when you reuse a view somewhere else in your app, or on a different-sized display.

`GeometryReader` dynamically reports size and position information about the parent view and the device, and updates whenever the size changes; for example, when the user rotates their iPhone.



You use `GeometryReader` to automatically identify the type and position of shape views in your app’s view hierarchy, such as `Circle`.

`GeometryReader` provides position information about the view’s parent view.

#### 2. What shape does the following drawing code create?

```swift
Path { 
  path in   path.move(to: CGPoint(x: 20, y: 0))   
  path.addLine(to: CGPoint(x: 20, y: 200))   
  path.addLine(to: CGPoint(x: 220, y: 200))   
  path.addLine(to: CGPoint(x: 220, y: 0))}
.fill(   
  .linearGradient(       
    Gradient(colors: [.green, .blue]),       
    startPoint: .init(x: 0.5, y: 0),       
    endPoint: .init(x: 0.5, y: 0.5)   
  )
)
```

> The original position is at up-left, and the x stands for distance of upright direction.

![A triangle with a gradient fill.](https://docs-assets.developer.apple.com/published/d0a86a3c870857994a67017c34a414bd/04990301@2x.png)

While the code *does* add three lines (sides) to the path, the path builder automatically adds a fourth line back to the starting point, creating a four-sided shape.

![A rectangle with a gradient fill.](https://docs-assets.developer.apple.com/published/f7b93426dfc3ec2bf4e7d0f2b51bca5c/04990302@2x.png)

The drawn shape does have four sides but they are of equal length, unlike this rectangle. Additionally, the gradient fill doesn’t start with blue at the top.

![A square with a gradient fill.](https://docs-assets.developer.apple.com/published/d28d02decf2c64421da69c6fc9f09edc/04990303@2x.png)

The path builder automatically adds a fourth line of equal length back to the starting point, creating a four-sided square.

## 6. Animating Views and Transitions

When using SwiftUI, you can individually animate changes to views, or to a view’s state, no matter where the effects are. SwiftUI handles all the complexity of these combined, overlapping, and interruptible animations for you.

In this tutorial, you’ll animate a view that contains a graph for tracking the hikes a user takes while using the Landmarks app. Using the `animation(_:)` modifier, you’ll see just how easy it is to animate a view.

### 1. Add Hiking Data to the App

Before you can add animation, you’ll need something to animate. In this section, you’ll import and model hiking data, and then add some prebuilt views for displaying that data statically in a graph.



### 2. Add Animations to Individual Views

When you use the `animation(_:)` modifier on an equatable view, SwiftUI animates any changes to animatable properties of the view. A view’s color, opacity, rotation, size, and other properties are all animatable. When the view isn’t equatable, you can use the `animation(_:value:)` modifier to start animations when the specified value changes.

> In `HikeView.swift`, turn on animation for the button’s rotation by adding an animation modifier that begins on changes of the `showDetail` value.
>
> Take SwiftUI for a spin. Try combining different animation effects to see what’s possible.

### 3. Animate the Effects of State Changes

Now that you’ve learned how to apply animations to individual views, it’s time to add animations in places where you change your state’s value.

Here, you’ll apply animations to all of the changes that occur when a user taps a button and toggles the `showDetail` state property.

> Wrap the call to `showDetail.toggle()` with a call to the `withAnimation` function.
>
> Both of the views affected by the `showDetail` property — the disclosure button and the `HikeDetail` view — now have animated transitions.

### 4. Customize View Transitions

By default, views transition on- and offscreen by fading in and out. You can customize this transition by using the `transition(_:)` modifier.

Switch to using the `move(edge:)` transition, so that the graph slides in and out from the same side.



### 5. Compose Animations for Complex Effects

The graph switches between three different sets of data when you click the buttons below the bars. In this section, you’ll use a composed animation to give the capsules that make up the graph a dynamic, rippling transition.

Observe how the custom animation provides a rippling effect when transitioning between graphs.

Be sure to unpin the preview before moving on to the next tutorial.

- How do you prevent the rotation effect from being animated in the following example?

```swift
Label("Graph", systemImage: "chevron.right.circle")    
	.labelStyle(.iconOnly)    
	.imageScale(.large)    
	.rotationEffect(.degrees(showDetail ? 90 : 0))    
	.scaleEffect(showDetail ? 1.5 : 1)    
	.padding()    
	.animation(.spring(), value: showDetail)
```



Pass `nil` to the `animation(_:value:)` modifier.

```swift
Label("Graph", systemImage: "chevron.right.circle")    
.labelStyle(.iconOnly)    
.imageScale(.large)    
.rotationEffect(.degrees(showDetail ? 90 : 0))    
.animation(nil, value: showDetail)    
.scaleEffect(showDetail ? 1.5 : 1)    
.padding()    
.animation(.spring(), value: showDetail)
```

You can animate rotations that you create using the `rotationEffect(_:)` modifier.



The `rotationEffect(_:)` modifier can’t be animated, so you don’t need to change the code to prevent animation.

You can animate rotations that you create using the `rotationEffect(_:)` modifier.



Shield the rotation from being animated by applying the `withoutAnimation(_:)` modifier.

```swift
Label("Graph", systemImage: "chevron.right.circle")    .labelStyle(.iconOnly)    .imageScale(.large)    .withoutAnimation {        $0.rotationEffect(.degrees(showDetail ? 90 : 0))    }    .scaleEffect(showDetail ? 1.5 : 1)    .padding()    .animation(.spring(), value: showDetail)
```

There isn’t a `withoutAnimation(_:)` modifier; you might be thinking of the `withAnimation(_:_:)` global function.

- What’s a quick way to test how an animation behaves during interruptions like state changes?



Add a breakpoint to the line that contains the `animation(_:value:)` modifier, then step through the animation frame-by-frame.

The debugger helps you step through and understand stack frames and instructions in your app, but it’s not a quick way to move through the stages of an animation.



Adjust the duration of the animation so that it runs long enough that you can observe and tune its fine details.

Making animations take longer is a quick and easily reversible change that’s effective for iterating on animations.



Call `sleep(100)` repeatedly to slow down the animation.

Because SwiftUI handles the intermediate states of animation on your behalf, there isn’t a good place to put a `sleep(_:)` loop, nor is it best practice to do so.



## 7. App Design and Layout



## 8. Composing Complex Interfaces

The category view for Landmarks shows a vertically scrolling list of horizontally scrolling landmarks. As you build this view and connect it to your existing views, you’ll explore how composed views can adapt to different device sizes and orientations.

### 1. Add a Category View

You can provide a different way to browse the landmarks by creating a view that sorts landmarks by category, while highlighting a featured landmark at the top of the view.

### 2. Create a Category List

The category view displays all categories in separate rows arranged in a vertical column for easier browsing. You do this by combining vertical and horizontal stacks, and adding scrolling to the list.

> In `Landmark.swift`, add a `Category` enumeration and a `category` property to the `Landmark` structure.
>
> The `landmarkData.json` file already includes a `category` value for each landmark with one of three string values. By matching the names in the data file, you can rely on the structure’s `Codable` conformance to load the data.
>
> The `Landmark.Category` case name identifies each item in the list, which must be unique among other categories because it’s an enumeration.

### 3. Create a Category Row

Landmarks displays each category in a row that scrolls horizontally. Add a new view type to represent the row, then display all the landmarks for that category in the new view.

Reuse parts of the `Landmark` view you created in [Creating and Combining Views](https://developer.apple.com/tutorials/swiftui/creating-and-combining-views) to create familiar previews of a landmark.

### 4. Complete the Category View

Add the rows and the featured image to the category home page.

Set the edge insets to zero on both kinds of landmark previews so the content can extend to the edges of the display.

### 5. Add Navigation Between Sections

With all of the differently categorized landmarks visible in the view, the user needs a way to reach each section in the app. Use the navigation and presentation APIs to make the category home, the detail view, and favorites list navigable from a tab view.

- Which view is the root view for the Landmarks app?



```
LandmarksApp
```

The `App` conformer acts as the entry point for the Landmarks app, but isn’t itself a view.



```
Landmarks
```

“Landmarks” is the name of the app. The implementation uses a more specific name that describes the role and structure of the home view.



```
ContentView
```

The `WindowGroup` scene defined in the app body declares `ContentView` as the root view of the app.



- How does the `ContentView` view use code from the rest of the app?



It reuses image assets for the different landmarks.

The category home view reuses the landmark images used elsewhere, but assets typically aren’t code. When you leverage existing code by composing a view out of other views, the data and images within that view often come along for the ride.



It uses the same syntax for modifiers and the same naming conventions for views.

Syntax and naming are common across the whole framework. The Landmarks app doesn’t add new syntax or naming conventions.



It connects all of the landmark views in a navigation hierarchy.

The Landmarks app is the sum of all its views, including navigation views.



- What’s the right code to turn a view into a navigation link?



```
NavigationLink(    LandmarkCard(landmark: landmark),    destination: LandmarksView(landmark: landmark))
```

`NavigationLink` uses a view builder closure for its destination, and another for its label.



```
NavigationLink {    LandmarkDetail(landmark: landmark)} label: {    LandmarkCard(landmark: landmark)}
```

Both the destination and the label appear in view builder closures.



```
NavigationLink {    LandmarkCard(landmark: landmark)}.navigationDestination(LandmarksView(landmark: landmark))
```

There isn’t a `navigationDestination(_:)` modifier because the destination is a required part of the navigation link.

Answer number 2 is correct

## 9. Working with UI Controls

In the Landmarks app, users can create a profile to express their personality. To give users the ability to change their profile, you’ll add an edit mode and design the preferences screen.

You’ll work with a variety of common user interface controls for data entry, and update the Landmarks model types whenever the user saves their changes.

### 1. Display a User Profile

The badge is just a graphic, so the text in `HikeBadge` along with the `accessibilityLabel(_:)` modifier make the meaning of the badge clearer to other users.

Note

The badge’s drawing logic produces a result that depends on the size of the frame in which it renders. To ensure the desired appearance, render in a frame of 300 x 300 points. To get the desired size for the final graphic, then scale the rendered result and place it in a comparably smaller frame.

### 2. Add an Edit Mode

Users need to toggle between viewing or editing their profile details. You’ll add an edit mode by adding an `EditButton` to the existing `ProfileHost`, and then creating a view with controls for editing individual values.

### 3. Define the Profile Editor

The user profile editor consists primarily of different controls that change individual details in the profile. Some items in the profile, like the badges, aren’t user-editable, so they don’t appear in the editor.

For consistency with the profile summary, you’ll add the profile details in the same order in the editor.

### 4. Delay Edit Propagation

To make it so edits don’t take effect until after the user exits edit mode, you use the draft copy of their profile during editing, then assign the draft copy to the real copy only when the user confirms an edit.

- How do you update a view when the editing state changes; for example, when a user taps Done after editing their profile?



```swift
struct EditableNameView: View {   
  @State var isEditing = false   
  @State var name = ""   
  var body: some View {      
    TextField("Name", text: $name)         
    .disabled(!isEditing)   
  }
}
```

The editability of a view comes from the environment, not a local state change.



```swift
struct EditableNameView: View {   
  @Environment(\.editMode) var mode   
  @State var name = ""   
  var body: some View {     
    TextField("Name", text: $name)         
    .disabled(mode?.wrappedValue == .inactive)   
  }
}
```

> Guess 
>
> binding mode to \.editmode
>
> when mode's wrappedValue == .inactive 
>
> .disabled will be triggered

The code checks the edit mode stored in the environment. Storing the edit mode in the environment makes it simple for multiple views to update when the user enters and exits edit mode.



```swift
struct EditableNameView: View {   
  @State var name = ""   
  var body: some View {      
    TextField("Name", text: $name)         
    .onEditingChanged { isEditing in            
    $0.disabled = !isEditing         
    }   
  }
}
```

You don’t use a callback to change your user interface when the user changes the editing state.



- When do you add an accessibility label using the `accessibility(label:)` modifier?



Always add an accessibility label to every view in your app.

Only add an accessibility label when the view is a meaningful part of your app’s user interface. Always test your app with VoiceOver on.



Add an accessibility label whenever doing so would make the meaning of a user interface element clearer to more users.

Always test your app with VoiceOver on, and then add accessibility labels to your app’s views as necessary.



Only use the `accessibility(label:)` modifier when you haven’t added a tag modifier to the view.

The tag modifier doesn’t affect how VoiceOver speaks a user-interface element to the user. Always test your app with VoiceOver on.



- **What’s the difference between a modal and non-modal view presentation?**



When you present a view modally, the source view sets the edit mode of the destination view.

SwiftUI propagates the current edit mode in the environment. Modal presentation is a type of navigation.



When you present a view non-modally, the destination view covers the source view and replaces the current navigation stack.

When you present a view non-modally SwiftUI adds the destination view to the navigation stack.



When you present a view modally, the destination view covers the source view and replaces the current navigation stack.

You present a view modally when you want to break out of your app’s normal flow.



## 10. Interfacing with UIKit

SwiftUI works seamlessly with the existing UI frameworks on all Apple platforms. For example, you can place UIKit views and view controllers inside SwiftUI views, and vice versa.

This tutorial shows you how to convert the featured landmark from the home screen to wrap instances of `UIPageViewController` and `UIPageControl`. You’ll use `UIPageViewController` to display a carousel of SwiftUI views, and use state variables and bindings to coordinate data updates throughout the user interface.



### 1. Create a View to Represent a UIPageViewController

To represent UIKit views and view controllers in SwiftUI, you create types that conform to the `UIViewRepresentable` and `UIViewControllerRepresentable` protocols. Your custom types create and configure the UIKit types that they represent, while SwiftUI manages their life cycle and updates them when needed.

### 2. Create the View Controller’s Data Source

In a few short steps, you’ve done a lot — the `PageViewController` uses a `UIPageViewController` to show content from a SwiftUI view. Now it’s time to enable swiping interactions to move from page to page.

### 3. Track the Page in a SwiftUI View’s State

To prepare for adding a custom `UIPageControl`, you need a way to track the current page from within `PageView`.

To do this, you’ll declare a `@State` property in `PageView`, and pass a binding to this property down to the `PageViewController` view. The `PageViewController` updates the binding to match the visible page.



### 4. Add a Custom Page Control

You’re ready to add a custom `UIPageControl` to your view, wrapped in SwiftUI `UIViewRepresentable` view.



- Which protocol do you use to bridge UIKit view controllers into SwiftUI?



```
UIViewRepresentable
```

Use the `UIViewRepresentable` protocol to bridge UIKit *views* into SwiftUI, not view controllers.



```
UIHostingController
```

Use the `UIHostingController` to bridge SwiftUI views into a UIKit view and view controller hierarchy.



```
UIViewControllerRepresentable
```

Create a structure that conforms to `UIViewControllerRepresentable` and implement the protocol requirements to include a `UIViewController` in your SwiftUI view hierarchy.



- Which protocol do you use to bridge UIKit view controllers into SwiftUI?



```
UIViewRepresentable
```

Use the `UIViewRepresentable` protocol to bridge UIKit *views* into SwiftUI, not view controllers.



```
UIHostingController
```

Use the `UIHostingController` to bridge SwiftUI views into a UIKit view and view controller hierarchy.



```
UIViewControllerRepresentable
```

Create a structure that conforms to `UIViewControllerRepresentable` and implement the protocol requirements to include a `UIViewController` in your SwiftUI view hierarchy.



- In which method do you create a delegate or data source for a `UIViewControllerRepresentable` type?



In the same `makeUIViewController(context:)` method where you create the `UIViewController`, because it uses the delegate or data source.

SwiftUI calls a different method to create the coordinating object before calling `makeUIViewController(context:)`. The coordinator is available as part of the `context` parameter inside `makeUIViewController(context:)`.



In the initializer for the `UIViewControllerRepresentable` type.

Always configure your objects and respond to changes from within the methods required by the `UIViewControllerRepresentable` protocol.



In the `makeCoordinator()` method.

Return an instance of the coordinator type from `makeCoordinator()`. SwiftUI manages its life cycle and provides it as part of the `context` parameter in other required methods.