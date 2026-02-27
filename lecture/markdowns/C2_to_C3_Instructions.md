# Instructions: C2_button.txt to C3_structure.txt

## Overview

This guide shows how to refactor C2_button.kt into C3_structure.kt by adding a top app bar, bottom navigation bar, and extracting the counter UI into a separate composable function.

---

## Step 1: Add New Imports

Add the following imports to the import section:

```kotlin
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.FavoriteBorder
import androidx.compose.material.icons.filled.Home
import androidx.compose.material3.BottomAppBar
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.Icon
import androidx.compose.material3.IconButton
import androidx.compose.material3.TopAppBar
import androidx.compose.runtime.Composable
```

**Why:** These imports provide the components needed for the top app bar, bottom navigation bar, icons, and the ability to create reusable composable functions.

---

## Step 2: Add @OptIn Annotation

Add the `@OptIn(ExperimentalMaterial3Api::class)` annotation before the `onCreate` method:

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
override fun onCreate(savedInstanceState: Bundle?) {
```

**Why:** TopAppBar is an experimental API, so we need to opt-in to use it.

---

## Step 3: Refactor Scaffold with App Bars

Replace the `setContent {}` block's Scaffold with the new structure:

```kotlin
setContent {
    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text("My Counter") },
            )
        },
        bottomBar = {
            BottomAppBar {
                Row(
                    modifier = Modifier.fillMaxWidth(),
                    horizontalArrangement = Arrangement.SpaceEvenly
                ) {
                    IconButton(
                        onClick = {}
                    ) {
                        Icon(Icons.Default.Home, contentDescription = "Home")
                    }
                    IconButton(
                        onClick = {}
                    ) {
                        Icon(Icons.Default.FavoriteBorder, contentDescription = "Home")
                    }
                }
            }
        }
    ) { innerPadding ->
        Counter(
            modifier = Modifier
                .fillMaxSize()
                .padding(innerPadding)
        )
    }
}
```

**Changes:**

- Added `topBar` parameter with a `TopAppBar` displaying "My Counter"
- Added `bottomBar` parameter with `BottomAppBar` containing two icon buttons (Home and Favorite)
- Replaced the original `Column` with a call to the `Counter()` composable function
- Passed modifier to `Counter()` for proper layout spacing

---

## Step 4: Extract Counter as a Separate Composable

Add a new composable function after the MainActivity class definition:

```kotlin
@Composable
fun Counter(modifier: Modifier = Modifier) {
    Column(
        modifier = modifier,
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(
            text = "Counter",
            fontSize = 30.sp
        )
        Button(onClick = { println("Clicked") }) {
            Text(
                text = "Add",
                fontSize = 20.sp
            )
        }
    }
}
```

**Why:**

- Makes the code more modular and reusable
- Separates concerns between layout structure and counter UI
- Allows the `Counter` function to accept a modifier parameter for flexible layout integration

---

## Summary of Changes

| Aspect            | C2_button.txt             | C3_structure.txt                     |
| ----------------- | ------------------------- | ------------------------------------ |
| **App Structure** | Simple Scaffold           | Scaffold with top and bottom bars    |
| **Top Bar**       | None                      | TopAppBar with "My Counter" title    |
| **Bottom Bar**    | None                      | BottomAppBar with 2 navigation icons |
| **Counter UI**    | Inline in MainActivity    | Extracted to Counter() composable    |
| **Imports**       | 15 imports                | 26 imports                           |
| **Functions**     | 1 (MainActivity.onCreate) | 2 (onCreate + Counter)               |
