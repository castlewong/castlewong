Generative Pre-trained Transformer Notes


Skeuomorphism Neumorphism

```Swift
import SwiftUI

struct SkeuomorphismClock: View {
    let calendar = Calendar.current
    let timer = Timer.publish(every: 1, on: .main, in: .common).autoconnect()

    var body: some View {
        ZStack {
            Color(.sRGB, red: 0.1, green: 0.1, blue: 0.1, opacity: 1.0).edgesIgnoringSafeArea(.all)
            VStack(spacing: 16) {
                Text(getHour())
                    .font(.system(size: 72, weight: .thin, design: .rounded))
                    .foregroundColor(.white)
                HStack(spacing: 8) {
                    Text(getMinute())
                        .font(.system(size: 36, weight: .thin, design: .rounded))
                        .foregroundColor(.white)
                    Text(getSecond())
                        .font(.system(size: 36, weight: .thin, design: .rounded))
                        .foregroundColor(.white)
                }
            }
        }
    }

    func getHour() -> String {
        let hour = calendar.component(.hour, from: Date())
        return String(format: "%02d", hour)
    }

    func getMinute() -> String {
        let minute = calendar.component(.minute, from: Date())
        return String(format: "%02d", minute)
    }

    func getSecond() -> String {
        let second = calendar.component(.second, from: Date())
        return String(format: "%02d", second)
    }
}

```

Append array

```swift
struct ContentView: View {
  
@Environment(\.managedObjectContext) private var viewContext
  
@FetchRequest(entity: MyEntity.entity(), sortDescriptors: []) var fetchedResults: FetchedResults<MyEntity>

@State private var myArray: [Double] = [1.0, 2.0, 3.0]

var body: some View {
        // Use the fetched results in your view
        VStack {
            Text("Number of fetched results: \(fetchedResults.count)")

            // Update the state of myArray by appending the count of fetched results
            Button("Append count to array") {
                let countAsDouble = Double(fetchedResults.count)
                myArray.append(countAsDouble)
            }
        }
    }
}
```
