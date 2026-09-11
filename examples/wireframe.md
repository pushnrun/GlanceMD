# Settings wireframe

:::wireframe
height: 620
viewport: desktop
viewports: phone, tablet, desktop
screen: settings
interactive: true

screen settings
  layout split

    section Account
      text heading "Account settings"
      text body "Update your preferences"

      image avatar
        ratio: 1:1
        placeholder: Profile image

      tabs settings-tabs
        tab profile "Profile"
        tab security "Security"
        tab billing "Billing"

      field display-name
        type: text
        label: Display name
        value: Alex Morgan

      field theme
        type: select
        label: Theme
        options: System, Light, Dark
        value: System

      field bio
        type: textarea
        label: Bio
        placeholder: Tell people a little about yourself

      row
        field notifications
          type: switch
          label: Notifications
          value: true

        field newsletter
          type: checkbox
          label: Email newsletter
          value: false

      row
        button cancel
          label: Cancel
          variant: secondary

        button save
          label: Save changes
          variant: primary
          action: goto saved

    aside Summary
      badge plan
        label: Free plan

      progress setup
        value: 75

      card profile-summary
        text strong "Profile completeness"
        text body "Add an avatar to finish setup."

      alert privacy
        tone: info
        text: Your profile is private by default

screen saved
  section Confirmation
    text heading "Changes saved"
    text body "Your settings have been updated."

    badge state
      label: Saved

    button back
      label: Back to settings
      variant: primary
      action: goto settings
:::
