---
title: "Create playlist"
action: music_assistant.create_playlist
domain: music_assistant
description: "Creates a new playlist in Music Assistant."
related_actions:
  - music_assistant.get_library
  - music_assistant.play_media
---

Use this action to create a new, empty playlist in Music Assistant, for example as the first step of a script that fills it.

The action returns the new playlist in a response variable, including its URI, which you can use in later steps of the same automation or script.

{% include actions/ui_header.md %}

To create a playlist from an automation or a script:

1. Go to {% my automations title="**Settings** > **Automations & scenes**" %}.
2. Open an existing automation or script, or select **Create automation** > **Create new automation**.
3. If you're setting up a new automation, add a trigger in the **When** section. Scripts don't need a trigger. They run when something else calls them.
4. In the **Then do** section, select **Add action**.
5. From the search box, search for and select **Music Assistant: Create playlist**.
6. Fill in the options you want to use.
7. Optionally, in the **Response variable** field, enter a name to store the new playlist in, such as `new_playlist`.
8. Select **Save**.

This action does not support targets. In the UI, you are not prompted to choose an area, device, entity, or label. You select the Music Assistant instance through the **Music Assistant instance** option instead.

### Options in the UI

{% options_ui %}
Music Assistant instance:
  description: The Music Assistant instance to create the playlist in.
Playlist name:
  description: The name of the new playlist.
Provider:
  description: The Music Assistant provider to create the playlist in. When omitted, it is created as a Music Assistant playlist. The playlist is added to your Music Assistant library either way.
Username:
  description: Create the playlist as this Music Assistant user. The playlist belongs to this user. When omitted, the playlist is created as the Home Assistant user who started the action, if that user is linked to a Music Assistant user.
{% endoptions_ui %}

{% include actions/yaml_header.md %}

In YAML, refer to this action as `music_assistant.create_playlist`. A basic example looks like this:

{% example %}
action: |
  action: music_assistant.create_playlist
  data:
    config_entry_id: 01JEXNDHT21V0BHJXM7A5SZANV
    name: "Party mix"
  response_variable: new_playlist
{% endexample %}

### Options in YAML

{% options_yaml %}
config_entry_id:
  description: The ID of the Music Assistant instance to create the playlist in. Select the instance from the dropdown in the visual editor, then switch to YAML to read the value.
  required: true
  type: string
name:
  description: The name of the new playlist.
  required: true
  type: string
provider:
  description: The instance ID or domain of the Music Assistant provider to create the playlist in, such as `builtin`. When omitted, it is created as a Music Assistant playlist. The playlist is added to your Music Assistant library either way.
  required: false
  type: string
username:
  description: Create the playlist as this Music Assistant user. The playlist belongs to this user. When omitted, the playlist is created as the Home Assistant user who started the action, if that user is linked to a Music Assistant user.
  required: false
  type: string
{% endoptions_yaml %}

## Response data

The action returns the new playlist with its `name`, `uri`, and `media_type`. You can pass the `uri` to other actions, such as [Play media](/actions/music_assistant.play_media/).

## Good to know

- Creating a playlist as a specific Music Assistant user requires Music Assistant server version 2.11 or later.

{% include actions/stuck.md %}

{% include actions/related.md %}
