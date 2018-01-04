###StatusAlert
链接：https://github.com/LowKostKustomz/StatusAlert
使用：
```
// Importing framework
import StatusAlert

// Creating StatusAlert instance
let statusAlert = StatusAlert.instantiate(withImage: UIImage(named: "Some image name"),
					  title: "StatusAlert title",
					  message: "Message to show beyond title",
					  canBePickedOrDismissed: isUserInteractionAllowed)

// Presenting created instance
statusAlert.show(in: viewShowAlertIn,
		 withVerticalPosition: .center(offset: 0))
```