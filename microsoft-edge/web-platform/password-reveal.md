---
description: Provides guidance on customizing the display of the password reveal button
title: Customize the password reveal button
author: MSEdgeTeam
ms.author: msedgedevrel
ms.date: 12/18/2020
ms.topic: article
ms.prod: microsoft-edge
keywords: microsoft edge, compatibility, web platform, password reveal, eye icon
---
# Customize the password reveal button  

The `password` input type in Microsoft Edge includes a **password reveal** button.  A user may choose the password input control to reveal the **password** field.  The revealed **password** field helps the user verify if the password is correctly.  After a user has entered text in the **password** field, a user may choose the **password reveal** button or select `Alt`+`F8` to toggle visibility of the input.  

:::row:::
   :::column span="":::
      A **password** field with dots hiding the characters entered by a user.  An eye-shaped icon displays to the right of the **password** field.
      
      :::image type="complex" source="../media/web-platform/password-reveal/password-eye.png" alt-text="The password reveal button is displayed next to the dots that hide the password text" lightbox="../media/web-platform/password-reveal/password-eye.png":::
         The password reveal button is displayed next to the dots that hide the password text  
      :::image-end:::  
   :::column-end:::
   :::column span="":::
      Choose the password reveal button to change the eye icon to an eye icon with a slash through it, and to reveal the original password text.  
      
      :::image type="complex" source="../media/web-platform/password-reveal/password-toggled.png" alt-text="The password reveal button has a slash on it and the original password text is displayed" lightbox="../media/web-platform/password-reveal/password-toggled.png":::
         The password reveal button has a slash on it and the original password text is displayed
      :::image-end:::  
   :::column-end:::
:::row-end:::  

By default, the **password reveal** button inserts into the Shadow DOM of all HTML `input` instances with the `type` set to `"password"`.  Starting with Microsoft Edge Version 87, users or [enterprises][DeployedgeMicrosoftEdgePoliciesPasswordrevealenabled] may disable this feature globally.  You, web designers and developers, should expect most Microsoft Edge users to have the default experience.  

## Remove the password reveal control  

You may completely remove the **password reveal** button by targeting the `::-ms-reveal` pseudo element.  

```css
::-ms-reveal {
    display: none;
}
```  

However, you should consider taking advantage of the **password reveal** button.  The native **password reveal** button has important [security measures](#visibility-of-the-control) built into the behavior.  

## Customize the control style  

Instead of fully removing the control, you may instead modify the styling of the **password reveal** button to better match the visual language of the website.  The following snippet provides an example of such styling.  

```css
::-ms-reveal {
    border: 1px solid transparent;
    border-radius: 50%;
    box-shadow: 0 0 3px currentColor;
}
```  

Keep the following things in mind when you style the **password reveal** button.  

*   The eye icon implements as a background image.  To add a background color to the **password reveal** button, use the CSS `background-color` property instead of the `background` shorthand property.  
*   You may adjust the size and scale of the **password reveal** button.  
    
    > [!NOTE]
    >The browser hides any overflow outside of the bounds of the password input control.  
    
*   Currently, no state selectors are available to style the toggled state of the **password reveal** button.  
    
## Visibility of the control  

The **password reveal** button is unavailable until the user enters text into the **password** field.  To help keep the user's password entry secure, the browser suppresses the button in the following scenarios.

*   If focus moves away from the **password** field, the browser removes the **password reveal** button.  
*   If scripts modify the **password** field, the browser removes the **password reveal** button.  
*   If a user removes the **password reveal** button, the user must delete the contents of the **password** field before the **password reveal** button displays again.  
    
    > [!NOTE]
    > This feature prevents someone from making a minor adjustment to view the password, should the user step away from an unlocked device.
    
The **password reveal** button is unavailable if the **password** field autofills using the password manager.  

<!-- links -->  

[DeployedgeMicrosoftEdgePoliciesPasswordrevealenabled]: /deployedge/microsoft-edge-policies#passwordrevealenabled "PasswordRevealEnabled - Microsoft Edge - Policies | Microsoft Docs"  