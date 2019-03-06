---
title: ID2D1Factory CreateTransformedGeometry methods
description: Transforms the specified geometry and stores the result as an ID2D1TransformedGeometry object.
ms.assetid: '71f26200-0f35-49d7-951d-2962768d16bc'
keywords: ["CreateTransformedGeometry methods Direct2D"]
topic_type:
- apiref
api_location:
- D2d1.dll
api_type:
- DllExport
---

# ID2D1Factory::CreateTransformedGeometry methods

Transforms the specified geometry and stores the result as an [**ID2D1TransformedGeometry**](https://msdn.microsoft.com/en-us/library/Dd371304(v=VS.85).aspx) object.

### Overload list



| Method                                                                                                                                                                                                                  | Description                                                                                                                                    |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------|
| [**CreateTransformedGeometry(ID2D1Geometry\*,D2D\_MATRIX\_3X2\_F\*,ID2D1TransformedGeometry\*\*)**](id2d1factory-createtransformedgeometry-ptr-id2d1geometry-ptr-d2d-matrix-3x2-f-ptr-ptr-https://msdn.microsoft.com/en-us/library/Dd371304(v=VS.85).aspx) | Transforms the specified geometry and stores the result as an [**ID2D1TransformedGeometry**](https://msdn.microsoft.com/en-us/library/Dd371304(v=VS.85).aspx) object. <br/> |
| [**CreateTransformedGeometry(ID2D1Geometry\*,D2D\_MATRIX\_3X2\_F&,ID2D1TransformedGeometry\*\*)**](id2d1factory-createtransformedgeometry-ptr-id2d1geometry-ref-d2d-matrix-3x2-f-ptr-ptr-https://msdn.microsoft.com/en-us/library/Dd371304(v=VS.85).aspx)  | Transforms the specified geometry and stores the result as an [**ID2D1TransformedGeometry**](https://msdn.microsoft.com/en-us/library/Dd371304(v=VS.85).aspx) object. <br/> |



## Remarks

Like other resources, a transformed geometry inherits the resource space and threading policy of the factory that created it. This object is immutable.

When stroking a transformed geometry with the [**DrawGeometry**](https://msdn.microsoft.com/en-us/library/Dd371890(v=VS.85).aspx) method, the stroke width is not affected by the transform applied to the geometry. The stroke width is only affected by the world transform.

## Examples

The following example creates an [**ID2D1RectangleGeometry**](https://msdn.microsoft.com/en-us/library/Dd371286(v=VS.85).aspx), then draws it without transforming it. It produces the output shown in the following illustration.

![illustration of a rectangle](images/transformedgeometry2-step1.png)


```C++
hr = m_pD2DFactory->CreateRectangleGeometry(
    D2D1::RectF(150.f, 150.f, 200.f, 200.f),
    &amp;m_pRectangleGeometry
    );
```



The next example uses the render target to scale the geometry by a factor of 3, then draws it. The following illustration shows the result of drawing the rectangle without the transform and with the transform; notices that the stroke is thicker after the transform, even though the stroke thickness is 1.

![illustration of a smaller rectangle inside a larger rectangle with a thicker stroke](images/transformedgeometry2-step2.png)


```C++
// Transform the render target, then draw the rectangle geometry again.
m_pRenderTarget->SetTransform(
    D2D1::Matrix3x2F::Scale(
        D2D1::SizeF(3.f, 3.f),
        D2D1::Point2F(175.f, 175.f))
    );

m_pRenderTarget->DrawGeometry(m_pRectangleGeometry, m_pBlackBrush, 1);
```



The next example uses the **CreateTransformedGeometry** method to scale the geometry by a factor of 3, then draws it. It produces the output shown in the following illustration. Notice that, although the rectangle is larger, its stroke hasn't increased.

![illustration of a smaller rectangle inside a larger rectangle with the same stroke](images/transformedgeometry2-step3.png)


```C++
 // Create a geometry that is a scaled version
 // of m_pRectangleGeometry.
 // The new geometry is scaled by a factory of 3
 // from the center of the geometry, (35, 35).

 hr = m_pD2DFactory->CreateTransformedGeometry(
     m_pRectangleGeometry,
     D2D1::Matrix3x2F::Scale(
         D2D1::SizeF(3.f, 3.f),
         D2D1::Point2F(175.f, 175.f)),
     &amp;m_pTransformedGeometry
     );
```

<span codelanguage="ManagedCPlusPlus"></span>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>C++</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>// Replace the previous render target transform.
m_pRenderTarget-&gt;SetTransform(D2D1::Matrix3x2F::Identity());

// Draw the transformed geometry.
m_pRenderTarget-&gt;DrawGeometry(m_pTransformedGeometry, m_pBlackBrush, 1);</code></pre></td>
</tr>
</tbody>
</table>



## Requirements



|                    |                                                                                     |
|--------------------|-------------------------------------------------------------------------------------|
| Header<br/>  | <dl> <dt>D2d1.h</dt> </dl>   |
| Library<br/> | <dl> <dt>D2d1.lib</dt> </dl> |
| DLL<br/>     | <dl> <dt>D2d1.dll</dt> </dl> |



## See also

<dl> <dt>

[**ID2D1Factory**](https://msdn.microsoft.com/en-us/library/Dd371246(v=VS.85).aspx)
</dt> </dl>

�

�




