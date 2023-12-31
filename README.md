## Discord#connect
args (if app ID not provided at compile time): Application ID (Integer)\
args (if app ID provided at compile time): none

Connect to Discord. You may provide an application ID at compile time by defining it as preprocessor macro `DISCORD_APPID`.

## Discord#update
args: none

Run Discord callbacks, should be called once per frame\
Here is an RGSS example
```Ruby
module Graphics
    class << self
        alias discord_update__ update unless method_defined?(:discord_update__)
    end

    def self.update
        Discord.update
        discord_update__
    end
end
```


## Discord#update_activity
args: Activity details (Hash)

Update discord activities/rich presence information\
here is an rgss example
```Ruby
Discord.update_activity({
    :details => "Overworld",
    :state => "The name of a map",
    :start_timestamp => 1507665886,
    :end_timestamp => 1507665936,
    :large_image => "large_image_cloud_asset_name",
    :large_image_text => "Large Image Text",
    :small_image => "small_image_cloud_asset_name",
    :small_image_text => "Small Image Text",
    :party_id => "ae488379-351d-4a4f-ad32-2b9b01c91657",
    :party_size => 5,
    :party_max => 6,
    :join_secret => "MTI4NzM0OjFpMmhuZToxMjMxMjM= "
})
```

You do not have to include every field here\
Please respect the data types or you will crash your game


## Discord#add_event_callback
args: Target event (Symbol), Callback (proc)

Add a proc to be called by the specified event\
The events are:

`:on_activity_join` -> fires when a user accepts an invite or receieves confirmation from asking to join\
`:on_activity_spectate` -> fires when a user accepts a spectate invite or clicks the spectate button on a user's profile\
`:on_activity_join_request` -> fires when a user asks to join the current user's game\
`:on_activity_invite` -> fires when the user receives a join or spectate invite

These events, alongside #send_request_reply, can be used to build rich multiplayer integration with Discord.


## Discord#send_request_reply
args: Joiner User ID (Integer), Discord::ActivityJoinRequestReply (NO, YES, IGNORE)

Returns Discord::Result via callback passed as block
