# Crystal Range Seekbar
[![](https://jitpack.io/v/hahn/crystal-range-seekbar.svg)](https://jitpack.io/#hahn/crystal-range-seekbar)

Please don't use this abandoned project. We only update this lib to support Androidx.

# Usage
Add a dependency to your `build.gradle`:
```groovy
dependencies {
    implementation 'com.github.hahn:crystal-range-seekbar:[LATEST_VERSION]'
}
```

# Features
- Customize with xml using custom handy attributes.
- Customize in your activity, fragment or dialog.
- Styling with your own widget.
- Creating newly widget from activity, fragment or dialog.

# Sample usage - Seekbar

Default style using xml.
```groovy
<com.crystal.crystalrangeseekbar.widgets.CrystalSeekbar
    android:id="@+id/rangeSeekbar1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"/>
```
---
![alt tag](https://drive.google.com/uc?export=view&id=0B9bDENyIABT6Snk1Q21TbjhkWjQ)

Styling with bubble animation using custom widget `BubbleThumbSeekbar`.
```groovy
<com.crystal.crystalrangeseekbar.widgets.BubbleThumbSeekbar
    android:id="@+id/rangeSeekbar2"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:corner_radius="10"
    app:min_value="50"
    app:max_value="150"
    app:bar_color="#C69E89"
    app:bar_highlight_color="#A54B17"
    app:left_thumb_color="#775E4F"
    app:left_thumb_color_pressed="#4C2D1A"
    app:data_type="_integer"/>
```
---

Styling with bubble animation with drawable using custom widget `BubbleThumbSeekbar`.
```groovy
<com.crystal.crystalrangeseekbar.widgets.BubbleThumbSeekbar
    android:id="@+id/rangeSeekbar3"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:corner_radius="10"
    app:min_value="0"
    app:max_value="100"
    app:steps="5"
    app:bar_color="#F7BB88"
    app:bar_highlight_color="#E07416"
    app:left_thumb_image="@drawable/thumb"
    app:left_thumb_image_pressed="@drawable/thumb_pressed"
    app:data_type="_integer"/>
```                    
---

Right to Left position (rtl)
```groovy
<com.crystal.crystalrangeseekbar.widgets.CrystalSeekbar
    android:id="@+id/rangeSeekbar7"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:position="right"/>
```                    
---

Right to Left position with drawable position update from code (rtl)
```groovy
<com.crystal.crystalrangeseekbar.widgets.CrystalSeekbar
    android:id="@+id/rangeSeekbar8"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:min_value="100"
    app:max_value="200"
    app:steps="5"
    app:bar_color="#F7BB88"
    app:bar_highlight_color="#E07416"
    app:left_thumb_image="@drawable/thumb"
    app:left_thumb_image_pressed="@drawable/thumb_pressed"
    app:data_type="_integer"/>
```                    
```java
// get seekbar from view
final CrystalSeekbar rangeSeekbar = (CrystalSeekbar) rootView.findViewById(R.id.rangeSeekbar8);

// change position left to right
rangeSeekbar.setPosition(CrystalSeekbar.Position.RIGHT).apply();
```
---

Create new seekbar from code and add to any view.
```java
// get seekbar from view
final CrystalSeekbar seekbar = new CrystalSeekbar(getActivity());

// get min and max text view
final TextView tvMin = (TextView) rootView.findViewById(R.id.textMin5);
final TextView tvMax = (TextView) rootView.findViewById(R.id.textMax5);

// set listener
seekbar.setOnSeekbarChangeListener(new OnSeekbarChangeListener() {
    @Override
    public void valueChanged(Number minValue) {
        tvMin.setText(String.valueOf(minValue));
    }
});

// set final value listener
seekbar.setOnSeekbarFinalValueListener(new OnSeekbarFinalValueListener() {
    @Override
    public void finalValue(Number value) {
        Log.d("CRS=>", String.valueOf(value));
    }
});
        
// get range seekbar container
RelativeLayout container = (RelativeLayout) rootView.findViewById(R.id.contRangeSeekbar5);
container.addView(rangeSeekbar);
```
---

Styling with create custom widget
```java
public class MySeekbar extends CrystalSeekbar {

    public MySeekbar(Context context) {
        super(context);
    }

    public MySeekbar(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    public MySeekbar(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    @Override
    protected float getMinValue(TypedArray typedArray) {
        return 5f;
    }

    @Override
    protected float getMaxValue(TypedArray typedArray) {
        return 90f;
    }

    @Override
    protected float getMinStartValue(TypedArray typedArray) {
        return 20f;
    }

    @Override
    protected int getBarColor(TypedArray typedArray) {
        return Color.parseColor("#A0E3F7");
    }

    @Override
    protected int getBarHighlightColor(TypedArray typedArray) {
        return Color.parseColor("#53C9ED");
    }

    @Override
    protected int getLeftThumbColor(TypedArray typedArray) {
        return Color.parseColor("#058EB7");
    }

    @Override
    protected int getLeftThumbColorPressed(TypedArray typedArray) {
        return Color.parseColor("#046887");
    }

    @Override
    protected Drawable getLeftDrawable(TypedArray typedArray) {
        return ContextCompat.getDrawable(getContext(), R.drawable.thumb);
    }

    @Override
    protected Drawable getLeftDrawablePressed(TypedArray typedArray) {
        return ContextCompat.getDrawable(getContext(), R.drawable.thumb_pressed);
    }
}
```

# Sample usage - Range Seekbar

Default style using xml.
```groovy
<com.crystal.crystalrangeseekbar.widgets.CrystalRangeSeekbar
    android:id="@+id/rangeSeekbar1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"/>
```

```java
// get seekbar from view
final CrystalRangeSeekbar rangeSeekbar = (CrystalRangeSeekbar) rootView.findViewById(R.id.rangeSeekbar1);

// get min and max text view
final TextView tvMin = (TextView) rootView.findViewById(R.id.textMin1);
final TextView tvMax = (TextView) rootView.findViewById(R.id.textMax1);

// set listener
rangeSeekbar.setOnRangeSeekbarChangeListener(new OnRangeSeekbarChangeListener() {
    @Override
    public void valueChanged(Number minValue, Number maxValue) {
        tvMin.setText(String.valueOf(minValue));
        tvMax.setText(String.valueOf(maxValue));
    }
});

// set final value listener
rangeSeekbar.setOnRangeSeekbarFinalValueListener(new OnRangeSeekbarFinalValueListener() {
    @Override
    public void finalValue(Number minValue, Number maxValue) {
        Log.d("CRS=>", String.valueOf(minValue) + " : " + String.valueOf(maxValue));
    }
});
```
---

Styling with bubble animation with drawable using custom widget `BubbleThumbRangeSeekbar`.
```groovy
<com.crystal.crystalrangeseekbar.widgets.BubbleThumbRangeSeekbar
    android:id="@+id/rangeSeekbar5"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:corner_radius="10"
    app:min_value="0"
    app:max_value="100"
    app:steps="5"
    app:bar_color="#F7BB88"
    app:bar_highlight_color="#E07416"
    app:left_thumb_image="@drawable/thumb"
    app:right_thumb_image="@drawable/thumb"
    app:left_thumb_image_pressed="@drawable/thumb_pressed"
    app:right_thumb_image_pressed="@drawable/thumb_pressed"
    app:data_type="_integer"/>
```
---
![alt tag](https://drive.google.com/uc?export=view&id=0B9bDENyIABT6bnZJWVZwUGV6TGc)

Set minimum range (gap).
```groovy
<com.crystal.crystalrangeseekbar.widgets.CrystalRangeSeekbar
    android:id="@+id/rangeSeekbar3"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:corner_radius="10"
    app:min_value="50"
    app:max_value="100"
    app:gap="20"
    app:bar_color="#8990C4"
    app:bar_highlight_color="#2434AD"
    app:left_thumb_color="#1A246D"
    app:right_thumb_color="#1A246D"
    app:left_thumb_color_pressed="#030B47"
    app:right_thumb_color_pressed="#030B47"
    app:data_type="_integer"/>
```
---

Set fix range (gap).
```groovy
<com.crystal.crystalrangeseekbar.widgets.CrystalRangeSeekbar
    android:id="@+id/rangeSeekbar4"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:corner_radius="10"
    app:min_value="0"
    app:max_value="100"
    app:fix_gap="30"
    app:bar_color="#EE88F7"
    app:bar_highlight_color="#D810EA"
    app:left_thumb_color="#8D0D99"
    app:right_thumb_color="#8D0D99"
    app:left_thumb_color_pressed="#56005E"
    app:right_thumb_color_pressed="#56005E"
    app:data_type="_integer"/>
```
---

__Available attributes__

+ ``corner_radius``: corner radius to be used seekbar, default ``0f``
+ ``min_value``: minimum value of seekbar, default ``0``
+ ``max_value``: maximum value of seekbar, default ``100``
+ ``min_start_value``: minimum start value must be equal or greater than min value, default ``min_value``
+ ``max_start_value``: maximum start value must be equal or less than max value, default ``max_value``
+ ``steps``: minimum steps between range, default NO_STEP ``-1f``
+ ``gap``: maintain minimum range between two thumbs, range must be greater >= min value && <= max value, default ``0f``
+ ``bar_height``: bar height, default determined by thumb size
+ ``fix_gap``: maintain fix range between two thumbs, range must be greater >= min value && <= max value, default NO_FIXED_GAP ``-1f``
+ ``bar_color_mode`` color fill mode of inactive bar; can be ``ColorMode.SOLID`` or ``ColorMode.GRADIENT``; default is ``ColorMode.SOLID``
+ ``bar_color`` inactive bar background color, default ``Color.GRAY``
+ ``bar_gradient_start`` inactive bar background gradient start color, default ``Color.GRAY``
+ ``bar_gradient_end`` inactive bar background gradient end color, default ``Color.DKGRAY``
+ ``bar_highlight_color_mode`` color fill mode of active bar; can be ``ColorMode.SOLID`` or ``ColorMode.GRADIENT``; default is ``ColorMode.SOLID``
+ ``bar_highlight_color`` active bar background color, default ``Color.BLACK``
+ ``bar_highlight_gradient_start`` active bar background gradient start color, default ``Color.DKGRAY``
+ ``bar_highlight_gradient_end`` active bar background gradient end color, default ``Color.BLACK``
+ ``thumb_color`` default thumb color, default ``Color.BLACK`` **(only CrystalSeekbar)**
+ ``thumb_color_pressed`` active thumb color, default ``Color.DKGRAY`` **(only CrystalSeekbar)**
+ ``thumb_image`` left drawable, default ``null`` **(only CrystalSeekbar)**
+ ``thumb_image_pressed`` active thumb drawable, default ``null`` **(only CrystalSeekbar)**
+ ``left_thumb_color`` default left thumb color, default ``Color.BLACK`` **(only CrystalRangeSeekbar)**
+ ``left_thumb_color_pressed`` active left thumb color, default ``Color.DKGRAY`` **(only CrystalRangeSeekbar)**
+ ``left_thumb_image`` left thumb drawable, default ``null`` **(only CrystalRangeSeekbar)**
+ ``left_thumb_image_pressed`` active left thumb drawable, default ``null`` **(only CrystalRangeSeekbar)**
+ ``right_thumb_color`` default right thumb color, default ``Color.BLACK`` **(only CrystalRangeSeekbar)**
+ ``right_thumb_color_pressed`` active right thumb color, default ``Color.DKGRAY`` **(only CrystalRangeSeekbar)**
+ ``right_thumb_image`` right thumb drawable, default ``null`` **(only CrystalRangeSeekbar)**
+ ``right_thumb_image_pressed`` active right thumb drawable, default ``null`` **(only CrystalRangeSeekbar)**
+ ``position`` can be ``left`` or ``right``, default ``left``
+ ``data_type`` can be ``_long`` or ``_double`` or ``_integer`` or ``_float`` or ``_short`` or ``_byte``, default ``_integer``

# LICENSE

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
