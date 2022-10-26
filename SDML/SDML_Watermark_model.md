[HOME](Home.md)
# Watermark Model #

```Swift
public enum SDMLWatermarkRotation {
    case no
    case clockwise
    case antiClockwise
}
```
```Swift
public class SDMLWatermark {
    var text: String
    var fontName: String = ""
    var fontColor: String = ""
    var fontSize: Int = 0
    var transparency: Int = 0
    var rotation: SDMLWatermarkRotation = .no
    var isRepeat: Bool = false
    
    public init() {
        self.text = ""
    }
    
    public init(text: String) {
        self.text = text
    }
}
```