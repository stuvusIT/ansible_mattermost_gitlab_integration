# mattermost-gitlab-integration

This role sets up a Mattermost GitLab integration service which posts changes of an organization or repository to a Mattermost channel.
For more information see [softdevteams repository](https://gitlab.com/softdevteam/mattermost-gitlab-integration).

## Requirements
This role requires an apt based system like Ubuntu.

## Role Variables

| Name                                           | Required/Default                         | Description                                                                                                      |
|:-----------------------------------------------|:----------------------------------------:|:-----------------------------------------------------------------------------------------------------------------|
| `mattermost_gitlab_integration_webhook_url`    | :heavy_check_mark:                       | Mattermost webhook url where the data should be send to                                                          |
| `mattermost_gitlab_integration_server_address` | `0.0.0.0`                                | Address of the server                                                                                            |
| `mattermost_gitlab_integration_server_port`    | `5000`                                   | Port under which the server listens to webhooks from gitlab                                                      |
| `mattermost_gitlab_integration_user`           | `www-data`                               | User under which the server should run. The user has to exist                                                    |
| `mattermost_gitlab_integration_group`          | `www-data`                               | Group under which the server should run. The group hast to exist                                                 |
| `mattermost_gitlab_integration_events`         | `[issue, comment, merge_request, build]` | List of events to be posted                                                                                      |
| `mattermost_gitlab_integration_username`       | ` `                                      | Username to post under in Mattermost                                                                             |
| `mattermost_gitlab_integration_icon_url`       | ` `                                      | URL to icon file which should show up in Mattermost                                                              |
| `mattermost_gitlab_integration_channel`        | ` `                                      | Leave this blank to post to the default channel of your webhook                                                  |
| `mattermost_gitlab_integration_verify_ssl`     | `true`                                   | Verify SSL certificates when POSTing to GitLab                                                                   |


### Events

Event                                                                                   | Enabled by default       | Variable name   |
----------------------------------------------------------------------------------------|--------------------------|-----------------|
[push](http://doc.gitlab.com/ee/web_hooks/web_hooks.html#comment-events)                | :heavy_multiplication_x: | `push`          |
[tag](https://docs.gitlab.com/ce/web_hooks/web_hooks.html#tag-events)                   | :heavy_multiplication_x: | `tag`           |
[issue](https://docs.gitlab.com/ce/web_hooks/web_hooks.html#issues-events)              | :heavy_check_mark:       | `issue`         |
[comment](https://docs.gitlab.com/ce/web_hooks/web_hooks.html#comment-events)           | :heavy_check_mark:       | `comment`       |
[merge request](http://doc.gitlab.com/ee/web_hooks/web_hooks.html#merge-request-events) | :heavy_check_mark:       | `merge_request` |
[build](https://docs.gitlab.com/ce/web_hooks/web_hooks.html#build-events)               | :heavy_check_mark:       | `build`         |

## Example Playbook

```yml
hosts: all
  become: true
  vars:
  mattermost_gitlab_integration_webhook_url: "https://yourwebhookurl.org"
    mattermost_gitlab_integration_server_address: 127.0.0.1
    mattermost_gitlab_integration_server_port: 5001
    mattermost_gitlab_integration_events: []
  roles:
    - mattermost-gitlab-integration
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

## Author Information

- [Fritz Otlinghaus (Scriptkiddi)](https://github.com/scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
