```swift
//
//  ContentView.swift
//  IVOPattern
//
//  Created by paige on 2021/11/16.
//

import SwiftUI

struct Profile: Identifiable {
    var id = UUID().uuidString
    var createdAt: Date
    var name: String
    
    init(createdAt: Date? = nil, name: String? = nil) {
        self.createdAt = createdAt ?? Date()
        self.name = name ?? ""
    }
        
}

struct ContentView: View {
    
    @StateObject private var observed = Observed()
    
    var body: some View {
        Text("Hello, \(observed.profile.name)")
            .onAppear {
                observed.fetchProfile { error in
                    
                }
            }
    }
}

extension ContentView {
    
    class Observed: ObservableObject {
        @Published var profile = Profile()
        func fetchProfile(completion: (Error?) -> ()) {
            let profile = Profile(name: "Alex")
            DispatchQueue.main.asyncAfter(deadline: .now()) {
                self.profile = profile
            }
        }
    }
    
}
```
