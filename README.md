# AndWheel
Android Wheel View, The original project may have stopped maintenance, I want to continue to maintain it, so I just fork it, made a few changes. In any case, this is not my credit. Let us pay tribute to our predecessors.

Original address: [https://code.google.com/archive/p/android-wheel](https://code.google.com/archive/p/android-wheel)

## Download
* Gradle
```
implementation 'com.yanzhenjie:wheel:1.0.0'
```

* Maven
```
<dependency>
  <groupId>com.yanzhenjie</groupId>
  <artifactId>wheel</artifactId>
  <version>1.0.0</version>
</dependency>
```

AndroidWheel requires at minimum Java 7 or Android 2.2(Api level 8) .

## Usage
1, Initialize View
```java
WheelView wheelView = ...;
```

2, Set the adapter
```java
WheelViewAdapter adapter = ...;
wheelView.setAdapter(adapter);
```

Adapter is an interface:
```java
public interface WheelViewAdapter {
    int getItemsCount();

    View getItem(int position, View convertView, ViewGroup parent);

    View getEmptyItem(View convertView, ViewGroup parent);

    void registerDataSetObserver(DataSetObserver observer);

    void unregisterDataSetObserver(DataSetObserver observer);
}
```

For convenience, AndWheel has provided some simple implementations of the adapter internally:
```java
1. AbstractWheelAdapter
2. AbstractWheelTextAdapter
3. ArrayWheelAdapter
4. NumericWheelAdapter
```
`AbstractWheelTextAdapter` is recommended.

3, Listening to the Item's changes
```java
wheelView.addChangingListener(new OnWheelChangedListener() {
    @Override
    public void onChanged(WheelView wheel, int oldValue, int newValue) {
        // TODO what to do.
    }
});
```
This oldValue/newValue is the `index` of the wheel's Item.

4, Listen to the Item's clicks
```java
wheelView.addClickingListener(new OnWheelClickedListener() {
    @Override
    public void onItemClicked(WheelView wheel, int itemIndex) {
        // TODO what to do.
    }
});
```

## Attached
The original project does not change the shadow of the View and middle selector. Now it works.

Modify the shadow above and below:
```java
int[] colors = new int[](Color.RED, Color.BLUE, Color.GREEN);

GradientDrawable topShadow = new GradientDrawable(GradientDrawable.Orientation.TOP_BOTTOM, colors);
wheelView.setTopShadow(topShadow);

GradientDrawable bottomShadow = new GradientDrawable(GradientDrawable.Orientation.BOTTOM_TOP, colors);
wheelView.setBottomShadow(bottomShadow);
```

Modify middle selector:
```java
Drawable centerFilter = ...;
wheelView.setCenterFilter(centerFilter);
```

This is an example: [https://github.com/yanzhenjie/Years](https://github.com/yanzhenjie/Years)

## ProGuard
If you are using ProGuard you might need to add the following options:
```
-dontwarn com.yanzhenjie.wheel.**
```

## License
```text
Copyright 2017 Yan Zhenjie

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```