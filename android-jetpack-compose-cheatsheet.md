# Android Jetpack Compose Cheatsheet

This comprehensive cheatsheet covers major UI and form-related components in Jetpack Compose, providing descriptions, summaries, and Kotlin code examples for each. 

## 1. Text
**Description/Summary**: The `Text` composable displays text on the screen. It supports styling options like color, font size, weight, style, alignment, and more, making it essential for labels, headings, and paragraphs.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.sp

@Composable
fun SimpleText() {
    Text(
        text = "Hello, Jetpack Compose!",
        color = Color.Blue,
        fontSize = 20.sp,
        fontWeight = FontWeight.Bold
    )
}
```

## 2. Button
**Description/Summary**: Buttons trigger actions. Jetpack Compose offers types like Filled, Tonal, Outlined, Elevated, and Text buttons, each with Material Design styling for emphasis levels (high, medium, low).

**Sample Kotlin Code** (Filled Button):
```kotlin
import androidx.compose.material3.Button
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable

@Composable
fun SimpleButton(onClick: () -> Unit) {
    Button(onClick = onClick) {
        Text("Click Me")
    }
}
```

## 3. Image
**Description/Summary**: The `Image` composable displays images from resources, bitmaps, or painters. It supports scaling, alpha, color filters, and shapes like circles.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.foundation.Image
import androidx.compose.runtime.Composable
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.layout.ContentScale

@Composable
fun SimpleImage() {
    Image(
        painter = painterResource(id = R.drawable.example_image),
        contentDescription = "Example Image",
        contentScale = ContentScale.Crop
    )
}
```

## 4. Column
**Description/Summary**: Arranges child composables vertically. Supports vertical arrangement (e.g., top, center, spaced) and horizontal alignment.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable

@Composable
fun SimpleColumn() {
    Column(verticalArrangement = Arrangement.Center) {
        Text("Item 1")
        Text("Item 2")
    }
}
```

## 5. Row
**Description/Summary**: Arranges child composables horizontally. Supports horizontal arrangement and vertical alignment.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable

@Composable
fun SimpleRow() {
    Row(horizontalArrangement = Arrangement.SpaceBetween) {
        Text("Left")
        Text("Right")
    }
}
```

## 6. Box
**Description/Summary**: A container for stacking or aligning single/multiple children. Useful for overlays, alignments, and custom drawings.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.size
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.unit.dp

@Composable
fun SimpleBox() {
    Box(modifier = Modifier.size(100.dp).background(Color.Red)) {
        // Child content here
    }
}
```

## 7. Spacer
**Description/Summary**: An empty space for adding gaps between composables. Defined by width, height, or size modifiers.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.width
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp

@Composable
fun SimpleSpacer() {
    Row {
        Text("Left")
        Spacer(modifier = Modifier.width(16.dp))
        Text("Right")
    }
}
```

## 8. Surface
**Description/Summary**: A Material Design container for applying themes, colors, elevations, and shapes. Ideal for cards or themed sections.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.graphics.Color

@Composable
fun SimpleSurface() {
    Surface(color = Color.LightGray) {
        Text("Content on Surface")
    }
}
```

## 9. Card
**Description/Summary**: A container for grouping related content with elevation, shape, and borders. Often used for items in lists.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.Card
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable

@Composable
fun SimpleCard() {
    Card {
        Text("Card Content")
    }
}
```

## 10. LazyColumn
**Description/Summary**: Efficiently renders scrolling vertical lists, loading only visible items. Similar to RecyclerView.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable

@Composable
fun SimpleLazyColumn(items: List<String>) {
    LazyColumn {
        items(items) { item ->
            Text(item)
        }
    }
}
```

## 11. Modifier
**Description/Summary**: Chainable extensions for customizing composables (e.g., padding, size, background). Essential for layouts and styling.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.unit.dp

@Composable
fun SimpleModifier() {
    Text(
        "Modified Text",
        modifier = Modifier
            .padding(16.dp)
            .background(Color.Yellow)
    )
}
```

## 12. TextField
**Description/Summary**: A basic input field for user text entry. Supports labels, placeholders, validation, and keyboard options like IME actions for form.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.TextField
import androidx.compose.runtime.Composable
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.ui.text.input.TextFieldValue

@Composable
fun SimpleTextField() {
    val text = remember { mutableStateOf(TextFieldValue("")) }
    TextField(
        value = text.value,
        onValueChange = { text.value = it },
        label = { androidx.compose.material3.Text("Enter text") }
    )
}
```

## 13. OutlinedTextField
**Description/Summary**: An outlined variant of TextField with borders, ideal for forms where multiple fields are grouped. Supports error states and icons.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.OutlinedTextField
import androidx.compose.runtime.Composable
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.ui.text.input.TextFieldValue

@Composable
fun SimpleOutlinedTextField() {
    val text = remember { mutableStateOf(TextFieldValue("")) }
    OutlinedTextField(
        value = text.value,
        onValueChange = { text.value = it },
        label = { androidx.compose.material3.Text("Name") }
    )
}
```

## 14. Checkbox
**Description/Summary**: A toggle for selecting multiple options in forms. Represents binary states (checked/unchecked) and can be grouped.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.Checkbox
import androidx.compose.runtime.Composable
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember

@Composable
fun SimpleCheckbox() {
    val checked = remember { mutableStateOf(false) }
    Checkbox(
        checked = checked.value,
        onCheckedChange = { checked.value = it }
    )
}
```

## 15. RadioButton
**Description/Summary**: Allows single selection from a group of options in forms. Typically used in a RadioGroup for mutual exclusivity.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.RadioButton
import androidx.compose.runtime.Composable
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember

@Composable
fun SimpleRadioButton(selected: Boolean, onSelect: () -> Unit) {
    RadioButton(
        selected = selected,
        onClick = onSelect
    )
}
```

## 16. Switch
**Description/Summary**: A toggle switch for binary settings in forms, like on/off states. Supports colors and thumb customization.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.Switch
import androidx.compose.runtime.Composable
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember

@Composable
fun SimpleSwitch() {
    val checked = remember { mutableStateOf(false) }
    Switch(
        checked = checked.value,
        onCheckedChange = { checked.value = it }
    )
}
```

## 17. Slider
**Description/Summary**: Allows users to select a value from a continuous or discrete range in forms. Customizable with steps, colors, and value ranges.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.Slider
import androidx.compose.runtime.Composable
import androidx.compose.runtime.mutableFloatStateOf
import androidx.compose.runtime.remember

@Composable
fun SimpleSlider() {
    val value = remember { mutableFloatStateOf(0f) }
    Slider(
        value = value.floatValue,
        onValueChange = { value.floatValue = it },
        valueRange = 0f..100f
    )
}
```

## 18. DropdownMenu
**Description/Summary**: A menu that drops down for selecting from a list of options in forms. Often used with ExposedDropdownMenuBox for text field integration.

**Sample Kotlin Code**:
```kotlin
import androidx.compose.material3.DropdownMenu
import androidx.compose.material3.DropdownMenuItem
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember

@Composable
fun SimpleDropdownMenu() {
    val expanded = remember { mutableStateOf(false) }
    DropdownMenu(
        expanded = expanded.value,
        onDismissRequest = { expanded.value = false }
    ) {
        DropdownMenuItem(onClick = {}, text = { Text("Option 1") })
    }
}
```
