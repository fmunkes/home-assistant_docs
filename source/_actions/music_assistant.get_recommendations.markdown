---
title: "Get recommendations"
action: music_assistant.get_recommendations
domain: music_assistant
description: "Retrieves the recommendations of Music Assistant."
related_actions:
  - music_assistant.get_library
  - music_assistant.play_media
---

Use this action to retrieve the recommendations Music Assistant shows on its home screen, such as recently played items, in rows. You can use them, for example, to build a dashboard of suggestions.

This action returns its result in a response variable, which you can use in later steps of the same automation or script. It does not change anything on a player.

{% include actions/ui_header.md %}

To use this action from an automation or a script:

1. Go to {% my automations title="**Settings** > **Automations & scenes**" %}.
2. Open an existing automation or script, or select **Create automation** > **Create new automation**.
3. If you're setting up a new automation, add a trigger in the **When** section. Scripts don't need a trigger. They run when something else calls them.
4. In the **Then do** section, select **Add action**.
5. From the search box, search for and select **Music Assistant: Get recommendations**.
6. Fill in the options you want to use.
7. In the **Response variable** field, enter a name to store the data in.
8. Select **Save**.

This action does not support targets. In the UI, you are not prompted to choose an area, device, entity, or label. You select the Music Assistant instance through the **Music Assistant instance** option instead.

### Options in the UI

{% options_ui %}
Music Assistant instance:
  description: The Music Assistant instance to use.
Username:
  description: Run the action as this Music Assistant user. When omitted, the action runs as the Home Assistant user who started it, if that user is linked to a Music Assistant user.
{% endoptions_ui %}

{% include actions/yaml_header.md %}

In YAML, refer to this action as `music_assistant.get_recommendations`. A basic example looks like this:

{% example %}
action: |
  action: music_assistant.get_recommendations
  data:
    config_entry_id: 01JEXNDHT21V0BHJXM7A5SZANV
  response_variable: result
{% endexample %}

### Options in YAML

{% options_yaml %}
config_entry_id:
  description: The ID of the Music Assistant instance to use. Select the instance from the dropdown in the visual editor, then switch to YAML to read the value.
  required: true
  type: string
username:
  description: Run the action as this Music Assistant user. When omitted, the action runs as the Home Assistant user who started it, if that user is linked to a Music Assistant user.
  required: false
  type: string
{% endoptions_yaml %}

## Response data

The action returns a `recommendations` list. Each row has a `name` and an `items` list with the media items in that row.

## Good to know

- Recommendations depend on the user: each Music Assistant user gets their own.
- Rows that Music Assistant hides by default, such as random items, are left out.
- This action requires Music Assistant server version 2.11 or later.

{% include actions/stuck.md %}

{% include actions/related.md %}
