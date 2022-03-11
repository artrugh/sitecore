## Rendering Parameters

Rendering Parameters are a **key-value** pair.

**Only one** Rendering parameters template can be assign to a **redering definition item**

They provide **Content Authors** the capability to set values parameters in Experience Editor.

Adding a **Rendering Parameters Template** is the best practice to set them, to avoid errors when the values are hardcoding.

### Add a new Rendering Parameters Template

- Go to Templates
- Add a new subfolder called **Rendering Parameters templates**
- right-click in the folder
- insert a new template
- select as base template: **Templates/System/Layout/Rendering Parameters/Standard Rendering Parameters**
- name it Parameters Template
- Open the template
- name the section Styles
- Add a Field called Bg-Color
- type Droplist

### Add Bg-Color Sample items

- go to home
- create a folder Rendering Parameters
- Inside create Folder Bg-Color
- Inside Insert a Sample Item
- Add Title blue
- create as many items as colors you want.

### Assing Source to Bg-Color Field in Rendering Parameters Template

- set the source field to the created folder which groups the color items: sitecore/Content/Rendering Parameters/Bg-Color

### Add the template to the component definition item

- scroll to the Parameters Template
- add the new Rendering Parameters Template

### Use the new parameter in the Rendering

```csharp
@RenderingContext.Current.Rendering.Parameters["Parameter-Key"]
```