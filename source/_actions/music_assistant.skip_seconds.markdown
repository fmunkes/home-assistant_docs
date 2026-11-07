---
title: "Skip seconds"
action: music_assistant.skip_seconds
domain: music_assistant
description: "Skips forward or back within the item a Music Assistant player is playing."
related_actions:
  - music_assistant.get_queue
  - music_assistant.play_media
---

Use this action to skip forward or back by a number of seconds within the item that a Music Assistant player is playing, for example 30 seconds in an audiobook or a podcast episode.

{% include actions/ui_header.md %}

To use this action from an automation or a script:

1. Go to {% my automations title="**Settings** > **Automations & scenes**" %}.
2. Open an existing automation or script, or select **Create automation** > **Create new automation**.
3. If you're setting up a new automation, add a trigger in the **When** section. Scripts don't need a trigger. They run when something else calls them.
4. In the **Then do** section, select **Add action**.
5. Select what you want to control. Under **By target** (see [Targets](#targets)), select the Music Assistant media player that is playing.
6. From the actions shown for that target, under **Music Assistant**, select **Skip seconds**.
7. Fill in the options you want to use.
8. Select **Save**.

### Options in the UI

{% options_ui %}
Seconds:
  description: The number of seconds to skip. A negative number skips back.
Username:
  description: Run the action as this Music Assistant user. When omitted, the action runs as the Home Assistant user who started it, if that user is linked to a Music Assistant user.
{% endoptions_ui %}

{% include actions/yaml_header.md %}

In YAML, refer to this action as `music_assistant.skip_seconds`. A basic example looks like this:

{% example %}
action: |
  action: music_assistant.skip_seconds
  target:
    entity_id: media_player.kitchen_speaker
  data:
    seconds: 30
{% endexample %}

This skips 30 seconds forward on the kitchen speaker.

### Options in YAML

{% options_yaml %}
seconds:
  description: The number of seconds to skip. A negative number skips back.
  required: true
  type: integer
username:
  description: Run the action as this Music Assistant user. When omitted, the action runs as the Home Assistant user who started it, if that user is linked to a Music Assistant user.
  required: false
  type: string
{% endoptions_yaml %}

{% include actions/targets.md domain="media_player" %}

## Good to know

- The player must be playing from its Music Assistant queue, and the item must have a known duration. A radio stream, for example, has none.
- Running the action as a specific Music Assistant user requires Music Assistant server version 2.11 or later.

{% include actions/try_it.md %}

{% include actions/stuck.md %}

{% include actions/related.md %}
