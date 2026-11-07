---
title: "Save queue as playlist"
action: music_assistant.save_queue_as_playlist
domain: music_assistant
description: "Saves the active queue of a Music Assistant player as a new playlist."
related_actions:
  - music_assistant.get_queue
  - music_assistant.play_media
---

Use this action to save the items in the active queue of a Music Assistant player as a new playlist in your Music Assistant library, for example to keep the mix you just played.

{% include actions/ui_header.md %}

To use this action from an automation or a script:

1. Go to {% my automations title="**Settings** > **Automations & scenes**" %}.
2. Open an existing automation or script, or select **Create automation** > **Create new automation**.
3. If you're setting up a new automation, add a trigger in the **When** section. Scripts don't need a trigger. They run when something else calls them.
4. In the **Then do** section, select **Add action**.
5. Select what you want to control. Under **By target** (see [Targets](#targets)), select the Music Assistant media player whose queue you want to save.
6. From the actions shown for that target, under **Music Assistant**, select **Save queue as playlist**.
7. Fill in the options you want to use.
8. Select **Save**.

### Options in the UI

{% options_ui %}
Playlist name:
  description: The name of the new playlist.
Username:
  description: Run the action as this Music Assistant user. When omitted, the action runs as the Home Assistant user who started it, if that user is linked to a Music Assistant user.
{% endoptions_ui %}

{% include actions/yaml_header.md %}

In YAML, refer to this action as `music_assistant.save_queue_as_playlist`. A basic example looks like this:

{% example %}
action: |
  action: music_assistant.save_queue_as_playlist
  target:
    entity_id: media_player.kitchen_speaker
  data:
    name: "Party mix"
{% endexample %}

This saves the kitchen speaker's queue as a playlist called Party mix.

### Options in YAML

{% options_yaml %}
name:
  description: The name of the new playlist.
  required: true
  type: string
username:
  description: Run the action as this Music Assistant user. When omitted, the action runs as the Home Assistant user who started it, if that user is linked to a Music Assistant user.
  required: false
  type: string
{% endoptions_yaml %}

{% include actions/targets.md domain="media_player" %}

## Good to know

- This action requires Music Assistant server version 2.11 or later.
- Music Assistant creates the playlist in the background, so it can take a moment before it shows up in your library.
- An empty queue can't be saved. Items that can't be part of a playlist are left out.

{% include actions/try_it.md %}

{% include actions/stuck.md %}

{% include actions/related.md %}
