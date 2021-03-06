# Poll Bot

Matrix bot to do polls. What more do you need?

![image](https://user-images.githubusercontent.com/5547783/60209177-029b8e80-9852-11e9-8aee-c91d7ccaaec1.png)

**Project status:** This was thought as a proof of concept rather than something I'm actually willing to maintain in the longer term. If you want to take it over, feel free to fork it. Otherwise I'm unlikely to find both time and motivation to work on it more than just merging PRs.

## Build

```bash
git clone https://github.com/babolivier/matrix-poll-bot.git
cd matrix-poll-bot
go build
```

## Run

```
./matrix-poll-bot --config /path/to/config.yaml
```

## Configure

See [config.sample.yaml](/config.sample.yaml).

## Docker

```bash
git clone https://github.com/babolivier/matrix-poll-bot.git
cd matrix-poll-bot
docker build -t matrix-poll-bot .
# Add a file named 'config.yaml' to /path/to/config/dir
docker run -v /path/to/config/dir:/data matrix-poll-bot
# For an automatic start on system boot, use this:
docker run --restart=always --name=matrix-poll-bot -d -v /path/to/config/dir:/data matrix-poll-bot
```

## Usage

1. Create a user for PollBot - a non-admin user is sufficient
```
/usr/local/bin/matrix-synapse-register-user <pollbot-user> <pollbot-password> 0
Sending registration request...
Success!
```

2. Create an access token for the PollBot
```
curl --data '{"identifier": {"type": "m.id.user", "user": "<pollbot-user>" }, "password": "<pollbot-password>", "type": "m.login.password", "device_id": "PollBot", "initial_device_display_name": "PollBot"}' https://matrix.<your-matrix-server>/_matrix/client/r0/login
{
    "access_token": "",
    "device_id": "PollBot",
    "home_server": "<your-matrix-server>",
    "user_id": "@<pollbot-user>:<your-domain>",
    "well_known": {
        "m.homeserver": {
            "base_url": "https://matrix.<your-domain>/"
        }
    }
}
```

3. Invite PollBot in the room you want to create polls
```
/invite @pollbot:<your-domain>
```

4. Create a poll
```
!poll <your-question>
<emoji-1> Answer 1
<emoji-2> Answer 2
<emoji-3> Answer 3
<...>
```

