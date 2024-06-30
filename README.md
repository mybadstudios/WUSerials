### WUSerials
Pre- or auto-generate any number of serials you want/need per product. Assign a serial automatically upon purchase, manually via a single click or distribute serials with physical copies. The serial system works in a way that encourages sharing but discourages piracy. 

Requires the [WordPress For Unity Bridge](https://mybadstudios.com/product/wordpress-bridge/).

<script data-name="BMC-Widget" data-cfasync="false" src="https://cdnjs.buymeacoffee.com/1.0.0/widget.prod.min.js" data-id="mybad" data-description="Support me on Buy me a coffee!" data-message="Thank you for visiting. If you enjoy what you see, perhaps you could buy me a coffee?" data-color="#FF813F" data-position="Right" data-x_margin="18" data-y_margin="18">
</script>

# The 60 second introduction

In contrast with the other <em>WordPress For Unity Bridge</em> extensions, the Bridge: Serials extension requires almost nothing for you to do in Unity at all and does most of what it does in the WordPress dashboard instead. To get started with the asset just install it into your project and (if you haven't already done so) upload and activate the wub_serials plugin on your WordPress website. (You only need to do this step once)



## So what is the Bridge: Serials extension exactly?

 Simply put, it allows you to pre-generate any number of serials you want and then pair them up with user accounts. Every user on your website has a unique ID and when they register with a valid serial that ID becomes linked to that serial. This means 4 very important things:

1 <strong>Nobody else can use that serial</strong> any more because It is already allocated to someone
2 <strong>That serial is linked to that specific game for that specific person's account</strong> thus spanning all current and future devices, even temporary ones like an internet café or a friend's phone
3 <strong>A serial only needs to be entered once per user</strong> on any one device then never again. At this point it is safe for the user to forget the serial number as he will never need it ever again, not even when contacting customer support
4 <strong>Sharing the game or selling it second hand makes absolutely no sense</strong>. The game cannot be played with a serial and the serial is linked to a user's account. The player would have to give up his entire account in order to allow for piracy. This would give all pirates access to the account username/password/email and all pirates would share a high score/game progress/in-game currency/ in-game purchases... It makes  no sense to pirate the game...

If a user ever decides to sell the game second hand they first have to contact you to ask you to remove the serial from their account. Now the person can give his serial to the person he is selling to or, if he has forgotten it, you can tell it to him before you remove it from his account. Once that serial is linked to a new account the original owner will now be unable to play. All his game data will still be stored on your servers but he will need to buy a new license before he can play again. At that time, as just mentioned, all previous scores/items/loot/whatever will be there, waiting.

***

# Simplicity in Unity

From within Unity, Bridge : Serials only exposes 3 functions to you:
1 <b>RegisterSerial</b><br>
    * If a customer owns a serial and has not yet registered the game then use this function to send the serial to the server.
    * It will then be linked to the account of the player who used it

2 <b>ValidateRegistration</b><br>

    * If at any time you wish to check if a game is registered to the logged in player, call this. It takes no parameters and will either return a bool named "valid" with a value of true or it will trigger your error response callback. 
    * This is useful at the start of the game or if you just want to inject random checks to minimize any kind of game hacks

3 <b>FetchSerialNumber</b><br>

    * Again, this takes no parameters, but be sure the user is logged in before you call this. <br>
    * <b>NOTE:<em>The serial is NOT needed for anything after registration so the results of this function are purely for you to use in some cosmetic fasion</em></b>

***

# Dashboard Control panel

* This asset includes a complete dashboard interface for generating and removing serials. 
* You can reserve serials for games being distributed in retail stores
* If you have the Bridge: Money extension installed you can also sell your games directly via your website
    * This results in non-reserved serials being allocated and registered to the buyer automatically upon purchase.
    * This means your customers never have to enter their serial even once, nor even know that they were ever even issued one.
    * Their game will be registered and ready for them to play from the moment your WooCommerce transaction completes
* View all available serials
* Delete or add new / more serials
* View all allocated serials per game
* View all serials belonging to a specific user
* Assign or revoke a serial to/from a specific user with a single click !

***

# Automatic Bridge Login integration

The demo login prefabs installed into your project when you installed the WordPress for Unity Bridge will automatically detect when the Bridge: Serials expansion is installed into your project and expose a couple of new fields to you

* <b>Bool Check_for_serial</b><br>
If true, the login process will check to see if that account has a registered serial linked to it and set the static value WULogin.HasSerial accordingly

* <b>Bool Fetch_serial</b><br>
If true, the registered serial will be returned after login

* <b>Bool Require_serial_for_login</b><br>
If true, it changes the behavior of the login prefab(s).
    * Instead of closing the prefab so players can start to play, if no valid serial was found it now redirects to a panel where they have to either register with a serial they have in their possession or (optionally) go to your website to buy one.<br>
    * The PostLoginMenu screen's "Continue playing" button now also does the same test

* <b>String Product_url</b><br>
Used by the button on the registration panel in case you want to sell your game from your website. 
    * By clicking that button users will be taken to the url you specify in this field
    * Defaults to your website home screen if not set, otherwise it redirects users to this absolute URL (example use: link directly to your game's product page)

***

# Automatic WooCommerce integration

All WooCommerce integration for all Bridge extensions is enabled by installing the<br>[http://mybadstudios.com/wordpress-systems/wumoney/](Bridge : Money plugin) on your website.

If you have that plugin installed and enabled then all you need to do to integrate Bridge : Serials into WooCommerce is to create a normal WooCommerce virtual, non-downloadable product and give it an SKU using the format WUSKU_GID_GAME (where GID is the actual Game ID of the game you are selling).<br>That is all. You are done!

By doing this, anyone who buys the game from your website will automatically be allocated a serial and have that serial registered to their account as soon as the transaction state is set to completed. All they need to do is log in and start playing. That simple...

***

# Static properties at your disposal

* <strong>Bool RequireSerialForLogin</strong><br>
    * Maps to the private "Check for serial" bool set in the inspector. 
    * Poll this to determine if a serial is required to continue past a certain point. 
    * Currently in use by the login function and "Resume game" buttons to either enter the game or display the registration panel.

* <strong>Bool HasSerial</strong><br>
    * Returns whether or not a serial is linked to this account. 
    * Works with the "Check for Serial" bool

* <strong>String SerialNumber</strong><br>
    * This property holds the player's serial number if "Fetch serial" was set to true

***

# USE CASE SCENARIOS

1. Enable <em>Require_serial_for_login</em> to force people to pay for the game before they can play. This means you can <strong>make your game available for free download</strong> and not have to worry about it.

2. Disable <em>Require_serial_for_login</em> and enable <em>Fetch_serial</em>. 
    * This will fetch the registered serial (if any) during login. 
    * By doing this you can do your serial checks (WULogin.HasSerial) manually and basically turn your complete game into a demo. 
    * Offer people:
        * a few free levels or
        * a few minutes of play or
        * let them play until they have done a specific task (like collect 5 flowers)
    * To get the full game they just have to pay on your website or enter a serial in the game
    * No extra downloading required to unlock the full game !

3. Disable <em>Require_serial_for_login</em> and enable <em>Fetch_serial</em>.
    * Use this to determine if a player has paid for your game
    * instead of locking the game after a few levels, unlock in-game bonus content only to paid up players:
        * Extra characters
        * unlimited ammo
        * half price in-game purchases
        * turn of ads etc.
    * Make the game free and earn your money via advertisements but provide an incentive for players to buy the game also or to disable ads. 
