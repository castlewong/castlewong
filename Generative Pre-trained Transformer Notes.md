Generative Pre-trained Transformer Notes



------

PieChart



import SwiftUI

struct PieChart: View {
    
    var dataEntries: [ChartData]
    var colors: [Color]
    
    var body: some View {
        ZStack {
            ForEach(0..<dataEntries.count, id: \.self) { index in
                PieChartSlice(startAngle: angle(for: index), endAngle: angle(for: index+1))
                    .fill(colors[index % colors.count])
            }
        }
    }
    
    func angle(for index: Int) -> Angle {
        guard !dataEntries.isEmpty else { return .zero }
        
        let total = dataEntries.reduce(0) { $0 + $1.value }
        var currentTotal: Double = 0.0
        
        for i in 0..<index {
            currentTotal += dataEntries[i].value
        }
        
        return .degrees(currentTotal / total * 360)
    }
}

struct PieChartSlice: Shape {
    
    var startAngle: Angle
    var endAngle: Angle
    
    func path(in rect: CGRect) -> Path {
        var path = Path()
        
        let center = CGPoint(x: rect.midX, y: rect.midY)
        let radius = min(rect.width, rect.height) / 2
        
        path.move(to: center)
        path.addArc(center: center, radius: radius, startAngle: startAngle, endAngle: endAngle, clockwise: false)
        path.closeSubpath()
        
        return path
    }
}

struct ChartData {
    let value: Double
}

struct PieChartView: View {
    
```swift
let chartData: [ChartData] = [
    ChartData(value: 45),
    ChartData(value: 30),
    ChartData(value: 25)
]

let colors: [Color] = [
    .red,
    .green,
    .blue
]

var body: some View {
    VStack {
        Text("Pie Chart")
            .font(.headline)
        PieChart(dataEntries: chartData, colors: colors)
            .frame(width: 200, height: 200)
    }
}
```
}

struct PieChart_Previews: PreviewProvider {
    static var previews: some View {
        PieChartView()
    }
}

------


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
