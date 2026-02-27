# Step-by-Step Instructions: C0_original.kt → C1_hello_world.kt

## Step 1: Remove unused imports

Delete the following import statements:

```kotlin
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.runtime.Composable
import androidx.compose.ui.tooling.preview.Preview
import com.example.counter68.ui.theme.Counter68Theme
```

## Step 2: Add new import

Add this import after the existing imports:

```kotlin
import androidx.compose.ui.unit.sp
```

## Step 3: Simplify onCreate() method

Replace the current `onCreate()` method body:

**FROM:**

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    enableEdgeToEdge()
    setContent {
        Counter68Theme {
            Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
                Greeting(
                    name = "Android",
                    modifier = Modifier.padding(innerPadding)
                )
            }
        }
    }
}
```

**TO:**

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContent {
        Scaffold() { innerPadding ->
            Text(
                text = "Hello World",
                modifier = Modifier.padding(innerPadding),
                fontSize = 30.sp
            )
        }
    }
}
```

## Step 4: Delete the Greeting() composable function

Remove the entire function:

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}
```

## Step 5: Delete the GreetingPreview() function

Remove the entire preview function:

```kotlin
@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    Counter68Theme {
        Greeting("Android")
    }
}
```
