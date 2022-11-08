## Quick/dirty way to set up LUKS with version 2 and dm-integrity:

`cryptsetup luksFormat --type luks2 /dev/sdwhatever --integrity hmac-sha256`
