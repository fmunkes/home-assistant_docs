---
title: "Remove queue item"
action: music_assistant.remove_queue_item
domain: music_assistant
description: "Removes an item from the active queue of a Music Assistant player."
related_actions:
  - music_assistant.get_queue
  - music_assistant.transfer_queue
---

Use this action to remove an item from the active queue of a Music Assistant player.

{% include actions/ui_header.md %}

To use this action from an automation or a script:

1. Go to {% my automations title="**Settings** > **Automations & scenes**" %}.
2. Open an existing automation or script, or select **Create automation** > **Create new automation**.
3. If you're setting up a new automation, add a trigger in the **When** section. Scripts don't need a trigger. They run when something else calls them.
4. In the **Then do** section, select **Add action**.
5. Select what you want to control. Under **By target** (see [Targets](#targets)), select the Music Assistant media player whose queue you want to change.
6. From the actions shown for that target, under **Music Assistant**, select **Remove queue item**.
7. Fill in the options you want to use.
8. Select **Save**.

### Options in the UI

{% options_ui %}
Queue item ID:
  description: The ID of the queue item. You can get it from the `queue_items` returned by the [Get queue details](/actions/music_assistant.get_queue/) action when you set its **Limit**.
Username:
  description: Run the action as this Music Assistant user. When omitted, the action runs as the Home Assistant user who started it, if that user is linked to a Music Assistant user.
{% endoptions_ui %}

{% include actions/yaml_header.md %}

In YAML, refer to this action as `music_assistant.remove_queue_item`. A basic example looks like this:

{% example %}
action: |
  action: music_assistant.remove_queue_item
  target:
    entity_id: media_player.kitchen_speaker
  data:
    queue_item_id: "5d95dc5be77e4f7eb4939f62cfef527b"
{% endexample %}

This removes the given item from the kitchen speaker's queue.

### Options in YAML

{% options_yaml %}
queue_item_id:
  description: The ID of the queue item. You can get it from the `queue_items` returned by the [Get queue details](/actions/music_assistant.get_queue/) action when you set its **Limit**.
  required: true
  type: string
username:
  description: Run the action as this Music Assistant user. When omitted, the action runs as the Home Assistant user who started it, if that user is linked to a Music Assistant user.
  required: false
  type: string
{% endoptions_yaml %}

{% include actions/targets.md domain="media_player" %}

## Good to know

- The item that is playing or about to play can't be removed. The action then has no effect.
- Running the action as a specific Music Assistant user requires Music Assistant server version 2.11 or later.

{% include actions/try_it.md %}

{% include actions/stuck.md %}

{% include actions/related.md %}
