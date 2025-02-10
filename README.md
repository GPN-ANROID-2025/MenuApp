#  Day 18 : MenuApp

```markdown
# Menus in Android (Java)

Android provides three types of menus: **Options Menu**, **Context Menu**, and **Popup Menu**.

## 1. Options Menu
The **Options Menu** appears in the app bar (overflow menu) when the user taps the three-dot menu.

### Example:
```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main, menu);
    return true;
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
    switch (item.getItemId()) {
        case R.id.action_settings:
            Toast.makeText(this, "Settings clicked", Toast.LENGTH_SHORT).show();
            return true;
        default:
            return super.onOptionsItemSelected(item);
    }
}
```
**menu_main.xml (res/menu/menu_main.xml)**:
```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/action_settings"
        android:title="Settings"
        android:showAsAction="never"/>
</menu>
```

## 2. Context Menu
The **Context Menu** appears when the user performs a long-press on a view.

### Example:
```java
@Override
public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
    super.onCreateContextMenu(menu, v, menuInfo);
    menu.add(0, v.getId(), 0, "Edit");
    menu.add(0, v.getId(), 0, "Delete");
}

@Override
public boolean onContextItemSelected(MenuItem item) {
    Toast.makeText(this, item.getTitle() + " selected", Toast.LENGTH_SHORT).show();
    return true;
}
```
**Registering the Context Menu**:
```java
TextView textView = findViewById(R.id.textView);
registerForContextMenu(textView);
```

## 3. Popup Menu
The **Popup Menu** appears as a floating menu anchored to a view.

### Example:
```java
PopupMenu popup = new PopupMenu(this, view);
popup.getMenuInflater().inflate(R.menu.popup_menu, popup.getMenu());
popup.setOnMenuItemClickListener(item -> {
    Toast.makeText(this, item.getTitle() + " clicked", Toast.LENGTH_SHORT).show();
    return true;
});
popup.show();
```
**popup_menu.xml (res/menu/popup_menu.xml)**:
```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/action_edit" android:title="Edit"/>
    <item android:id="@+id/action_delete" android:title="Delete"/>
</menu>
```

Each menu serves different use cases:
- **Options Menu**: For app-wide actions.
- **Context Menu**: For actions related to a specific view (long-press).
- **Popup Menu**: For quick actions related to a view (button click).

```
