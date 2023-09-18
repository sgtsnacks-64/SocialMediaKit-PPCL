# The Social Media Kit
# How theming works?

## Introduction

Urgh! Another Theming methodology in Canvas Apps!

This guide sets out to be a compehensive runthrough on how the theming of the components held in "The Social Media Kit" works, to arm you with all the methods available to get the most out of this component library.

## The Principle

Records in Power Apps Canvas Apps can generally contain as much, or as little, content as needed. As there is no mechanism of "Required" vs "Optional" fields when declaring records, we can use this to our advantage to create a flexible theming system which compromises of *Defaults* and *Overrides*.

```javascript
{
//Defaults
    Value1: "Hello",        //This is required
    Value2: "World",        //This is required
    
//Overrides    
    Override:
        {
            Value1: "Hi!"   //This would override the Default "Value1"
        }
}
```
## An overview of the Properties Record

Add any of the components from "The Social Media Kit" into your Canvas App and have a look at the "Properties" property. You should see an overwhelming-looking record value, don't panic!:
```javascript
{
    /*
            -----Default Style information, Will apply to all controls unless specified in the controls field below.
    */
    Colours: {
        Primary: ColorValue("#005d99"),         //Covers Fills for Actionable Controls (i.e. Buttons, Toggles, Checkboxes), Icon Colours
        Secondary: ColorValue("#555555"),       //Covers secondary colour accents
        Border: ColorValue("#005d99"),          //Specifically for border colours of controls such as text boxes, drop downs
        Background: Color.White,                 //Covers the background of the component itself, for Controls, this will control the Fill property
        Text: Color.Black
    },
    Style: {
        Borders: {
            Thickness: 1,
            FocusThickness: 1.0,
            Radius: {
                TopLeft: 0,
                TopRight: 0,
                BottomLeft: 0,
                BottomRight: 0
            }
        },
        Font: {
            'Font-Family': Font.'Open Sans',
            Sizes: {
                Heading: 28,
                Action: 16,
                Text: 17
            }
        }
    },
    /*
            ----End of Default configuration
    */
    Controls: {
        /*
                -----Overrides for individual control types in components. Options specified here will override the default options above.
        */
        Label: {
            Colours: {
                Primary: ColorValue("#005d99"),
                Secondary: ColorValue("#555555"),
                Border: ColorValue("#222222"),
                Background: RGBA(
                    0,
                    0,
                    0,
                    0
                ),
                Text: Color.Black
            },
            Style: {
                Borders: {
                    Thickness: 0.5,
...
}
```

This Record Property can be broken down into two sections. The first section (the top half) is the *defaults* section, and the second is the *override* section. This has been broken with comment blocks for visibility.

## Defaults

A theme must cover most, if not all controls and generally speaking, most, if not all settings. In this theming system, all control properties are mapped to the *defaults* section of the Properties Record. The *defaults* consists of the top portion of the Properties record object and resides in the root (as in, 0 levels deep) of the record:
```javascript
    /*
            -----Default Style information, Will apply to all controls unless specified in the controls field below.
    */
    Colours: {
        Primary: ColorValue("#005d99"),         //Covers Fills for Actionable Controls (i.e. Buttons, Toggles, Checkboxes), Icon Colours
        Secondary: ColorValue("#555555"),       //Covers secondary colour accents 
        Border: ColorValue("#005d99"),          //Specifically for border colours of controls such as text boxes, drop downs
        Background: Color.White,                 //Covers the background of the component itself, for Controls, this will control the Fill property
        Text: Color.Black
    },
    Style: {
        Borders: {
            Thickness: 1,
            FocusThickness: 1.0,
            Radius: {
                TopLeft: 0,
                TopRight: 0,
                BottomLeft: 0,
                BottomRight: 0
            }
        },
        Font: {
            'Font-Family': Font.'Open Sans',
            Sizes: {
                Heading: 28,
                Action: 16,
                Text: 17
            }
        }
    },
    /*
            ----End of Default configuration
    */
```

Makers are able to modify the settings in this section, and in turn these changes can be utlised in **any** of the components found in the Component Library. The defaults consist of three different 5 Colours:
* Primary Colour
* Secondary Colour
* Border Colour
* Background Colour
* Text Colour

Some Limited Border Controls:
* Thickness
* Focus Thickness
* Radius (Top Left, Top Right, Bottom Left, Bottom Right)

Some limited Typography Controls:
* Font Family
* Font Sizes (Heading +, Text |, Action -)

In some cases, this may be all the required theming you'll need to cover both components and controls you may add in addition to your apps.

However, for instances where you need more granular control over components. You can incorporate *overrides*.

## Overrides

Components consist of one or more controls. With this theming system, makers can control the look and feel of controls within a component by utilising overrides.

Overrides work by adding a "Controls" field to the root of the Properties record, and then nesting specific control names within the Controls field.

In the following example, we have a component that contains a Label control. We want to change the text colour of the Label to **Color.Red**, but we wish for all other controls in all other components to utilise the "Default" configuration of **Color.Black**.

```javascript
{
    /*
            -----Default Style information, Will apply to all controls unless specified in the controls field below.
    */
    Colours: {
        Primary: ColorValue("#005d99"),         //Covers Fills for Actionable Controls (i.e. Buttons, Toggles, Checkboxes), Icon Colours
        Secondary: ColorValue("#555555"),       //Covers secondary colour accents 
        Border: ColorValue("#005d99"),          //Specifically for border colours of controls such as text boxes, drop downs
        Background: Color.White,                 //Covers the background of the component itself, for Controls, this will control the Fill property
        Text: Color.Black
    },
    Style: {
        Borders: {
            Thickness: 1,
            FocusThickness: 1.0,
            Radius: {
                TopLeft: 0,
                TopRight: 0,
                BottomLeft: 0,
                BottomRight: 0
            }
        },
        Font: {
            'Font-Family': Font.'Open Sans',
            Sizes: {
                Heading: 28,
                Action: 16,
                Text: 17
            }
        }
    },
    /*
            ----End of Default configuration
    */
    Controls: {
        /*
                -----Overrides for individual control types in components. Options specified here will override the default options above.
        */
        Label: {
            Colours: {
                Text: Color.Red
            }
        }
    }
}

```

Notice if you observe the default "Property" record from the component, the Controls records are populated with all the same properties you find in the "Default" configuration. However, when specifing overrides into the component, not all properties have to be addressed. In the example above, we're only assigning the **Text Colour** of **label** to **Color.Red**. 

Each component has a ReadMe text input property, which denotes the controls that can be overidden:

```javascript
/*

****Toolbar Component****
****The Social Media Kit****

Controls that can be overidden:

+ Gallery
+ TextInput
+ Icon
+ Label
...

*/
```

## How to use the Properties Record in your app

It makes little sense to have individual Properties Records configured on each component in an app, as this would exponentially increase the administration of theming. So it's advised to set the contents of the "Properies Record" to either a Global Variable, or a Collection if you wish to offer more than one theme to your users. This can be done in App.OnStart(), a Screen.OnVisible() or via another behaviour method.

```javascript
/*
    Setting the default theme to a Global Variable
*/
App.OnStart = 
    Set(
        gvTheme,
        {
        /*
                -----Default Style information, Will apply to all controls unless specified in the controls field below.
        */
        Colours: {
            Primary: ColorValue("#005d99"),         //Covers Fills for Actionable Controls (i.e. Buttons, Toggles, Checkboxes), Icon Colours
            Secondary: ColorValue("#555555"),       //Covers secondary colour accents 
            Border: ColorValue("#005d99"),          //Specifically for border colours of controls such as text boxes, drop downs
            Background: Color.White,                 //Covers the background of the component itself, for Controls, this will control the Fill property
            Text: Color.Black
        },
        Style: {
            Borders: {
                Thickness: 1,
                FocusThickness: 1.0,
                Radius: {
                    TopLeft: 0,
                    TopRight: 0,
                    BottomLeft: 0,
                    BottomRight: 0
                }
            },
            Font: {
                'Font-Family': Font.'Open Sans',
                Sizes: {
                    Heading: 28,
                    Action: 16,
                    Text: 17
                }
            }
        }
    })
```

You can set the "Properties" value of each component to the variable defined, and the component will adhere to the theme 
```javascript
Component.Properties = gvTheme
```


