---
title: "Add to playlist"
action: music_assistant.add_to_playlist
domain: music_assistant
description: "Adds items to a playlist in the Music Assistant library."
related_actions:
  - music_assistant.get_library
  - music_assistant.search
---

Use this action to add tracks or other items to a playlist in your Music Assistant library, for example to collect the songs you like from a dashboard button.

{% include actions/ui_header.md %}

To add items to a playlist from an automation or a script:

1. Go to {% my automations title="**Settings** > **Automations & scenes**" %}.
2. Open an existing automation or script, or select **Create automation** > **Create new automation**.
3. If you're setting up a new automation, add a trigger in the **When** section. Scripts don't need a trigger. They run when something else calls them.
4. In the **Then do** section, select **Add action**.
5. From the search box, search for and select **Music Assistant: Add to playlist**.
6. Fill in the options you want to use.
7. Select **Save**.

This action does not support targets. In the UI, you are not prompted to choose an area, device, entity, or label. You select the Music Assistant instance through the **Music Assistant instance** option instead.

### Options in the UI

{% options_ui %}
Music Assistant instance:
  description: The Music Assistant instance the playlist is in.
Playlist:
  description: The URI of a playlist in the Music Assistant library, such as `library://playlist/12`. You can get it from the [Get library items](/actions/music_assistant.get_library/) action.
Media URI:
  description: The URI or URIs of the items to add, for example from the [Search Music Assistant](/actions/music_assistant.search/) action.
Username:
  description: Edit the playlist as this Music Assistant user. Only playlists this user may edit can be changed. When omitted, the playlist is edited as the Home Assistant user who started the action, if that user is linked to a Music Assistant user.
{% endoptions_ui %}

{% include actions/yaml_header.md %}

In YAML, refer to this action as `music_assistant.add_to_playlist`. A basic example looks like this:

{% example %}
action: |
  action: music_assistant.add_to_playlist
  data:
    config_entry_id: 01JEXNDHT21V0BHJXM7A5SZANV
    playlist: "library://playlist/12"
    media_id:
      - "spotify://track/1234"
{% endexample %}

### Options in YAML

{% options_yaml %}
config_entry_id:
  description: The ID of the Music Assistant instance the playlist is in. Select the instance from the dropdown in the visual editor, then switch to YAML to read the value.
  required: true
  type: string
playlist:
  description: The URI of a playlist in the Music Assistant library, starting with `library://playlist/`. You can get it from the [Get library items](/actions/music_assistant.get_library/) action.
  required: true
  type: string
media_id:
  description: The URI or URIs of the items to add.
  required: true
  type: [string, list]
username:
  description: Edit the playlist as this Music Assistant user. Only playlists this user may edit can be changed. When omitted, the playlist is edited as the Home Assistant user who started the action, if that user is linked to a Music Assistant user.
  required: false
  type: string
{% endoptions_yaml %}

This example adds the item that is playing on the kitchen speaker to a playlist, using the [Get queue details](/actions/music_assistant.get_queue/) action to find it:

{% example %}
script: |
  sequence:
    - action: music_assistant.get_queue
      target:
        entity_id: media_player.kitchen_speaker
      response_variable: queue_info
    - action: music_assistant.add_to_playlist
      data:
        config_entry_id: 01JEXNDHT21V0BHJXM7A5SZANV
        playlist: "library://playlist/12"
        media_id: "{{ queue_info['media_player.kitchen_speaker'].current_item.media_item.uri }}"
{% endexample %}

## Good to know

- Only playlists in the Music Assistant library can be changed. A playlist from a streaming provider must be added to the library first.
- Music Assistant adds the items in the background, so it can take a moment before they show up in the playlist. Errors while adding them, such as an item that can't be part of a playlist, are not reported back to Home Assistant.
- Editing a playlist as a specific Music Assistant user requires Music Assistant server version 2.11 or later.

{% include actions/stuck.md %}

{% include actions/related.md %}
