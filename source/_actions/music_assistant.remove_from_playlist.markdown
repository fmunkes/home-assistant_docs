---
title: "Remove from playlist"
action: music_assistant.remove_from_playlist
domain: music_assistant
description: "Removes items from a playlist in the Music Assistant library."
related_actions:
  - music_assistant.add_to_playlist
  - music_assistant.get_library
---

Use this action to remove items from a playlist in your Music Assistant library. You address the items by their position in the playlist, which the [Get item contents](/actions/music_assistant.get_item_contents/) action returns for each item.

{% include actions/ui_header.md %}

To remove items from a playlist from an automation or a script:

1. Go to {% my automations title="**Settings** > **Automations & scenes**" %}.
2. Open an existing automation or script, or select **Create automation** > **Create new automation**.
3. If you're setting up a new automation, add a trigger in the **When** section. Scripts don't need a trigger. They run when something else calls them.
4. In the **Then do** section, select **Add action**.
5. From the search box, search for and select **Music Assistant: Remove from playlist**.
6. Fill in the options you want to use.
7. Select **Save**.

This action does not support targets. In the UI, you are not prompted to choose an area, device, entity, or label. You select the Music Assistant instance through the **Music Assistant instance** option instead.

### Options in the UI

{% options_ui %}
Music Assistant instance:
  description: The Music Assistant instance the playlist is in.
Playlist:
  description: The URI of a playlist in the Music Assistant library, such as `library://playlist/12`.
Positions:
  description: The positions of the items to remove, as returned by the Get item contents action.
Username:
  description: Edit the playlist as this Music Assistant user. Only playlists this user may edit can be changed.
{% endoptions_ui %}

{% include actions/yaml_header.md %}

In YAML, refer to this action as `music_assistant.remove_from_playlist`. A basic example looks like this:

{% example %}
action: |
  action: music_assistant.remove_from_playlist
  data:
    config_entry_id: 01JEXNDHT21V0BHJXM7A5SZANV
    playlist: "library://playlist/12"
    positions:
      - 3
      - 7
{% endexample %}

### Options in YAML

{% options_yaml %}
config_entry_id:
  description: The ID of the Music Assistant instance the playlist is in. Select the instance from the dropdown in the visual editor, then switch to YAML to read the value.
  required: true
  type: string
playlist:
  description: The URI of a playlist in the Music Assistant library, starting with `library://playlist/`.
  required: true
  type: string
positions:
  description: The positions of the items to remove, as returned by the Get item contents action. Positions start at 1.
  required: true
  type: [integer, list]
username:
  description: Edit the playlist as this Music Assistant user. Only playlists this user may edit can be changed. When omitted, the playlist is edited as the Home Assistant user who started the action, if that user is linked to a Music Assistant user.
  required: false
  type: string
{% endoptions_yaml %}

## Good to know

- Only playlists in the Music Assistant library can be changed.
- Positions refer to the playlist as it is when you retrieve them. Retrieve them again if the playlist may have changed in between.
- Music Assistant removes the items in the background, so it can take a moment before the playlist is updated.
- Editing a playlist as a specific Music Assistant user needs a Music Assistant server newer than 2.10.

{% include actions/stuck.md %}

{% include actions/related.md %}
