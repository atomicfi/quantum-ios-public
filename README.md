# QuantumIOS

## Example

```swift
import UIKit
import WebKit
import QuantumIOS

class ViewController: UIViewController {
	@IBOutlet weak var webView: WKWebView!
	var quantum: Quantum?


	override func viewDidLoad() {
		super.viewDidLoad()
		webView.isInspectable = true

		// Initialize a quantum instance
		let quantum = Quantum()

		Task {
			// quantum.initialize takes two parameters.
			// 1. A WebView that uses the qauntum-js package to manage browsers (see example webapp)
			// 2. A UIViewController to present the browsers on top of
			// The WebView could be an existing web application you present to your users inside of your native app
			// or a hidden WebView that is used to house a web application that uses quantum-js to manage browsers
			let quantumToken = "YOUR_TOKEN_PROVIDED_FROM_ATOMIC"
			try await quantum.initialize(token: quantumToken, view: webView, controller: self)

			// If you haven't already navigated your webView to your website you can use quantum to do so
			let success = try await quantum.goto(url: "http://localhost:3000")
			print("LOADED: \(success)")
		}
	}
}
```
