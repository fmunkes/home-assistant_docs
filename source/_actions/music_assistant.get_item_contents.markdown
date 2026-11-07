---
title: "Get item contents"
action: music_assistant.get_item_contents
domain: music_assistant
description: "Retrieves the tracks, albums, or episodes of a Music Assistant item."
related_actions:
  - music_assistant.get_library
  - music_assistant.play_media
---

Use this action to list what an item contains: the tracks of an album or playlist, the albums or tracks of an artist, or the episodes of a podcast. The list is paged, so you can retrieve long playlists in parts.

This action returns its result in a response variable, which you can use in later steps of the same automation or script. It does not change anything on a player.

{% include actions/ui_header.md %}

To use this action from an automation or a script:

1. Go to {% my automations title="**Settings** > **Automations & scenes**" %}.
2. Open an existing automation or script, or select **Create automation** > **Create new automation**.
3. If you're setting up a new automation, add a trigger in the **When** section. Scripts don't need a trigger. They run when something else calls them.
4. In the **Then do** section, select **Add action**.
5. From the search box, search for and select **Music Assistant: Get item contents**.
6. Fill in the options you want to use.
7. In the **Response variable** field, enter a name to store the data in.
8. Select **Save**.

This action does not support targets. In the UI, you are not prompted to choose an area, device, entity, or label. You select the Music Assistant instance through the **Music Assistant instance** option instead.

### Options in the UI

{% options_ui %}
Music Assistant instance:
  description: The Music Assistant instance to use.
Media URI:
  description: The URI of the album, playlist, artist, or podcast.
Artist contents:
  description: For an artist, whether to return its albums or its tracks.
Limit:
  description: The maximum number of items to return.
Offset:
  description: The point in the list to start returning items from.
Username:
  description: Run the action as this Music Assistant user.
{% endoptions_ui %}

{% include actions/yaml_header.md %}

In YAML, refer to this action as `music_assistant.get_item_contents`. A basic example looks like this:

{% example %}
action: |
  action: music_assistant.get_item_contents
  data:
    config_entry_id: 01JEXNDHT21V0BHJXM7A5SZANV
    media_id: "library://playlist/12"
    limit: 50
  response_variable: result
{% endexample %}

### Options in YAML

{% options_yaml %}
config_entry_id:
  description: The ID of the Music Assistant instance to use. Select the instance from the dropdown in the visual editor, then switch to YAML to read the value.
  required: true
  type: string
media_id:
  description: The URI of the album, playlist, artist, or podcast, such as `library://playlist/12`.
  required: true
  type: string
media_type:
  description: For an artist, whether to return its albums (`album`) or its tracks (`track`). Ignored for other items.
  required: false
  type: string
  default: album
limit:
  description: The maximum number of items to return.
  required: false
  type: integer
  default: 25
offset:
  description: The point in the list to start returning items from.
  required: false
  type: integer
  default: 0
username:
  description: Run the action as this Music Assistant user. When omitted, the action runs as the Home Assistant user who started it, if that user is linked to a Music Assistant user.
  required: false
  type: string
{% endoptions_yaml %}

## Response data

The action returns an `items` list along with the `limit` and `offset` you requested. Each item includes its `name`, `uri`, and `media_type`, and its `position` in the album, playlist, or podcast.

## Good to know

- This action needs a Music Assistant server newer than 2.10.

{% include actions/stuck.md %}

{% include actions/related.md %}
