### setHeading(heading : Number, callback : Function)

The Set Heading command tells Sphero to adjust it's orientation, by
commanding a new reference heading (in degrees).

If stabilization is enabled, Sphero will respond immediately to this.

**Params:**

- `heading` (Number) Sphero's new reference heading, in degrees (0-359)
- `callback` (Function) function to be triggered after writing

### setStabilization(flag : Number, callback : Function)

The Set Stabilization command turns Sphero's internal stabilization on or
off, depending on the flag provided.

**Params:**

- `flag` (Number) stabilization setting flag (0 - off, 1 - on)
- `callback` (Function) function to be triggered after writing

### setRotationRate(rotation : Number, callback : Function)

The Set Rotation Rate command allows control of the rotation rate Sphero
uses to meet new heading commands.

A lower value offers better control, but with a larger turning radius.

Higher values yield quick turns, but Sphero may lose control.

The provided value is in units of 0.784 degrees/sec.

**Params:**

- `rotation` (Number) new rotation rate (0-255)
- `callback` (Function) function to be triggered after writing

### getChassisId(callback : Function)

The Get Chassis ID command returns the 16-bit chassis ID Sphero was
assigned at the factory.

**Params:**

- `callback` (Function) function to be triggered with a response

### setChassisId(chassisId : Number, callback : Function)

The Set Chassis ID command assigns Sphero's chassis ID, a 16-bit value.

This command only works if you're at the factory.

**Params:**

- `chassisId` (Number) new chassis ID
- `callback` (Function) function to be triggered after writing

### selfLevel(opts : Object, callback : Function)

The Self Level command controls Sphero's self-level routine.

This routine attempts to achieve a horizontal orientation where pitch/roll
angles are less than the provided Angle Limit.

After both limits are satisfied, option bits control sleep, final
angle(heading), and control system on/off.

An asynchronous message is returned when the self level routine completes.

For more detail on options, see the Sphero API documentation.

**Params:**

- `opts` (Object) self-level routine options
- `callback` (Function) function to be triggered after writing

### setDataStreaming(opts : Object, callback : Function)

The Set Data Streaming command configures Sphero's built-in support for
asynchronously streaming certain system and sensor data.

This command selects the internal sampling frequency, packet size,
parameter mask, and (optionally) the total number of packets.

These options are provided as an object, with the following properties:

- **n** - divisor of the maximum sensor sampling rate
- **m** - number of sample frames emitted per packet
- **mask1** - bitwise selector of data sources to stream
- **pcnt** - packet count 1-255 (or 0, for unlimited streaming)
- **mask2** - bitwise selector of more data sources to stream (optional)

For more explanation of these options, please see the Sphero API
documentation.

**Params:**

- `opts` (Object) object containing streaming data options
- `callback` (Function) function to be triggered after writing

### configureCollisions(opts : Object, cb : Function)

The Configure Collisions command configures Sphero's collision detection
with the provided parameters.

These include:

- **meth** - which detection method to use. Supported methods are 0x01,
  0x02, and 0x03 (see the collision detection document for details). 0x00
  disables this service.
- **xt, yt** - 8-bit settable threshold for the X (left, right) and
  y (front, back) axes of Sphero. 0x00 disables the contribution of that
  axis.
- **xs, ys** - 8-bit settable speed value for X/Y axes. This setting is
  ranged by the speed, than added to `xt` and `yt` to generate the final
  threshold value.
- **dead** - an 8-bit post-collision dead time to prevent re-triggering.
  Specified in 10ms increments.

**Params:**

- `opts` (Object) object containing collision configuration opts
- `cb` (Function) function to be triggered after writing

### configureLocator(opts : Object, callback : Function)

The Configure Locator command configures Sphero's streaming location data
service.

The following options must be provided:

- **flags** - bit 0 determines whether calibrate commands auto-correct the
  yaw tare value. When false, positive Y axis coincides with heading 0.
  Other bits are reserved.
- **x, y** - the current (x/y) coordinates of Sphero on the ground plane in
  centimeters
- **yawTare** - controls how the x,y-plane is aligned with Sphero's heading
  coordinate system. When zero, yaw = 0 corresponds to facing down the
  y-axis in the positive direction. Possible values are 0-359 inclusive.

**Params:**

- `opts` (Object) object containing locator service configuration
- `callback` (Function) function to be triggered after writing

### setAccelRange(idx : Number, callback : Function)

The Set Accelerometer Range command tells Sphero what accelerometer range
to use.

By default, Sphero's solid-state accelerometer is set for a range of ±8Gs.
You may wish to change this, perhaps to resolve finer accelerations.

This command takes an index for the supported range, as explained below:

IDX | Range
--- | -----
0   | ±2Gs
1   | ±4Gs
2   | ±8Gs (default)
3   | ±16Gs

**Params:**

- `idx` (Number) what accelerometer range to use
- `callback` (Function) function to be triggered after writing

### readLocator(callback : Function)

The Read Locator command gets Sphero's current position (X,Y), component
velocities, and speed-over-ground (SOG).

The position is a signed value in centimeters, the component velocities are
signed cm/sec, and the SOG is unsigned cm/sec.

**Params:**

- `callback` (Function) function to be triggered with data

### setRGBLed(opts : Object, callback : Function)

The Set RGB LED command sets the colors of Sphero's RGB LED.

An object containaing `red`, `green`, and `blue` values must be provided.

If `opts.flag` is set to 1 (default), the color is persisted across power
cycles.

**Params:**

- `opts` (Object) object containing RGB values for Sphero's LED
- `callback` (Function) function to be triggered after writing

### setBackLed(brightness : Number, callback : Function)

The Set Back LED command allows brightness adjustment of Sphero's tail
light.

This value does not persist across power cycles.

**Params:**

- `brightness` (Number) brightness to set to Sphero's tail light
- `callback` (Function) function to be triggered after writing

### getRGBLed(callback : Function)

The Get RGB LED command fetches the current "user LED color" value, stored
in Sphero's configuration.

This value may or may not be what's currently displayed by Sphero's LEDs.

**Params:**

- `callback` (Function) function to be triggered after writing

### roll(speed : Number, heading : Number, [state] : Number, callback : Function)

The Roll command tells Sphero to roll along the provided vector.

Both a speed and heading are required, the latter is considered relative to
the last calibrated direction.

Permissible heading values are 0 to 359 inclusive.

**Params:**

- `speed` (Number) what speed Sphero should roll at
- `heading` (Number) what heading Sphero should roll towards (0-359)
- `[state]` (Number) optional state parameter
- `callback` (Function) function to be triggered after writing

### boost(boost : Number, callback : Function)

The Boost command executes Sphero's boost macro.

It takes a 1-byte parameter, 0x01 to start boosting, or 0x00 to stop.

**Params:**

- `boost` (Number) whether or not to boost (1 - yes, 0 - no)
- `callback` (Function) function to be triggered after writing

### setRawMotors(opts : Object, callback : Function)

The Set Raw Motors command allows manual control over one or both of
Sphero's motor output values.

Each motor (left and right requires a mode and a power value from 0-255.

This command will disable stabilization is both mode's aren't "ignore", so
you'll need to re-enable it once you're done.

Mode | Description
---- | -----------
0x00 | Off (motor is open circuit)
0x01 | Forward
0x02 | Reverse
0x03 | Brake (motor is shorted)
0x04 | Ignore (motor mode and power is left unchanged

**Params:**

- `opts` (Object) object with mode/power values (e.g. lmode, lpower)
- `callback` (Function) function to be triggered after writing

### setMotionTimeout(time : Number, callback : Function)

The Set Motion Timeout command gives Sphero an ultimate timeout for the
last motion command to keep Sphero from rolling away in the case of
a crashed (or paused) application.

This defaults to 2000ms (2 seconds) upon wakeup.

**Params:**

- `time` (Number) timeout length in milliseconds
- `callback` (Function) function to be triggered when done writing

### setPermOptionFlags(flags : Array, callback : Function)

The Set Permanent Option Flags command assigns Sphero's permanent option
flags to the provided values, and writes them immediately to the config
block.

See below for the bit definitions.

**Params:**

- `flags` (Array) permanent option flags
- `callback` (Function) function to be triggered when done writing

### getPermOptionFlags(callback : Function)

The Get Permanent Option Flags command returns Sphero's permanent option
flags, as a bit field:

Bit # | Description
----- | -----------
0     | Set to prevent Sphero from immediately going to sleep when placed in the charger and connected over Bluetooth.
1     | Set to enable Vector Drive, that is, when Sphero is stopped and a new roll command is issued it achieves the heading before moving along it.
2     | Set to disable self-leveling when Sphero is inserted into the charger.
3     | Set to force the tail LED always on.
4     | Set to enable motion timeouts (see DID 02h, CID 34h)
5     | Set to enable retail Demo Mode (when placed in the charger, ball runs a slow rainbow macro for 60 minutes and then goes to sleep).
6     | Set double tap awake sensitivity to Light
7     | Set double tap awake sensitivity to Heavy
8     | Enable gyro max async message (NOT SUPPORTED IN VERSION 1.47)
6-31  | Unassigned

**Params:**

- `callback` (Function) function triggered with option flags data

### setTempOptionFlags(flags : Array, callback : Function)

The Set Temporary Option Flags command assigns Sphero's temporary option
flags to the provided values. These do not persist across power cycles.

See below for the bit definitions.

**Params:**

- `flags` (Array) permanent option flags
- `callback` (Function) function to be triggered when done writing

### getTempOptionFlags(callback : Function)

The Get Temporary Option Flags command returns Sphero's temporary option
flags, as a bit field:

Bit # | Description
----- | -----------
0     | Enable Stop On Disconnect behavior
1-31  | Unassigned

**Params:**

- `callback` (Function) function triggered with option flags data

### getConfigBlock(id : Number, callback : Function)

The Get Configuration Block command retrieves one of Sphero's configuration
blocks.

The response is a simple one; an error code of 0x08 is returned when the
resources are currently unavailable to send the requested block back. The
actual configuration block data returns in an asynchronous message of type
0x04 due to its length (if there is no error).

ID = 0x00 requests the factory configuration block
ID = 0x01 requests the user configuration block, which is updated with
current values first

**Params:**

- `id` (Number) which configuration block to fetch
- `callback` (Function) function to be triggered after writing

### setSSBModBlock(pwd : Number, block : Array, callback : Function)

The Set SSB Modifier Block command allows the SSB to be patched with a new
modifier block - including the Boost macro.

The changes take effect immediately.

**Params:**

- `pwd` (Number) a 32 bit (4 bytes) hexadecimal value
- `block` (Array) array of bytes with the data to be written
- `callback` (Function) a function to be triggered after writing

### setDeviceMode(mode : Number, callback : Function)

The Set Device Mode command assigns the operation mode of Sphero based on
the supplied mode value.

- **0x00**: Normal mode
- **0x01**: User Hack mode. Enables ASCII shell commands, refer to the
  associated document for details.

**Params:**

- `mode` (Number) which mode to set Sphero to
- `callback` (Function) function to be called after writing

### setConfigBlock(block : Array, callback : Function)

The Set Config Block command accepts an exact copy of the configuration
block, and loads it into the RAM copy of the configuration block.

The RAM copy is then saved to flash.

The configuration block can be obtained by using the Get Configuration
Block command.

**Params:**

- `block` (Array) - An array of bytes with the data to be written
- `callback` (Function) - To be triggered when done

### getDeviceMode(callback : Function)

The Get Device Mode command gets the current device mode of Sphero.

Possible values:

- **0x00**: Normal mode
- **0x01**: User Hack mode.

**Params:**

- `callback` (Function) function to be called with response

### getSSB(callback : Function)

The Get SSB command retrieves Sphero's Soul Block.

The response is simple, and then the actual block of soulular data returns
in an asynchronous message of type 0x0D, due to it's 0x440 byte length

**Params:**

- `callback` (Function) function to be called with response

### setSSB(pwd : Number, block : Array, callback : Function)

The Set SSB command sets Sphero's Soul Block.

The actual payload length is 0x404 bytes, but if you use the special DLEN
encoding of 0xff, Sphero will know what to expect.

You need to supply the password in order for it to work.

**Params:**

- `pwd` (Number) a 32 bit (4 bytes) hexadecimal value
- `block` (Array) array of bytes with the data to be written
- `callback` (Function) a function to be triggered after writing

### refillBank(type : Number, callback : Function)

The Refill Bank command attempts to refill either the Boost bank (0x00) or
the Shield bank (0x01) by attempting to deduct the respective refill cost
from the current number of cores.

If it succeeds, the bank is set to the maximum obtainable for that level,
the cores are spent, and a success response is returned with the lower core
balance.

If there aren't enough cores available to spend, Sphero responds with an
EEXEC error (0x08)

**Params:**

- `type` (Number) what bank to refill (0 - Boost, 1 - Shield)
- `callback` (Function) function to be called with response

### buyConsumable(id : Number, qty : Number, callback : Function)

The Buy Consumable command attempts to spend cores on consumables.

The consumable ID is given (0 - 7), as well as the quantity requested to
purchase.

If the purchase succeeds, the consumable count is increased, the cores are
spent, and a success response is returned with the increased quantity and
lower balance.

If there aren't enough cores available to spend, or the purchase would
exceed the max consumable quantity of 255, Sphero responds with an EEXEC
error (0x08)

**Params:**

- `id` (Number) what consumable to buy
- `qty` (Number) how many consumables to buy
- `callback` (Function) function to be called with response

### useConsumable(id : Number, callback : Function)

The Use Consumable command attempts to use a consumable if the quantity
remaining is non-zero.

On success, the return message echoes the ID of this consumable and how
many of them remain.

If the associated macro is already running, or the quantity remaining is
zero, this returns an EEXEC error (0x08).

**Params:**

- `id` (Number) what consumable to use
- `callback` (Function) function to be called with response

### grantCores(pw : Number, qty : Number, flags : Number, callback : Function)

The Grant Cores command adds the supplied number of cores.

If the first bit in the flags byte is set, the command immediately commits
the SSB to flash. Otherwise, it does not.

All other bits are reserved.

If the password is not accepted, this command fails without consequence.

**Params:**

- `pw` (Number) 32-bit password
- `qty` (Number) 32-bit number of cores to add
- `flags` (Number) 8-bit flags byte
- `callback` (Function) function to be triggered with response

### addXp(pw : Number, qty : Number, callback : Function)

The Grant XP command increases XP by adding the supplied number of minutes
of drive time, and immediately commits the SSB to flash.

If the password is not accepted, this command fails without consequence.

**Params:**

- `pw` (Number) 32-bit password
- `qty` (Number) 8-bit number of minutes of drive time to add
- `callback` (Function) function to be triggered with response

### levelUpAttr(pw : Number, id : Number, callback : Function)

The Level Up Attribute command attempts to increase the level of the
specified attribute by spending attribute points.

The IDs are:

- **0x00**: speed
- **0x01**: boost
- **0x02**: brightness
- **0x03**: shield


If successful, the SSB is committed to flash, and a response packet
containing the attribute ID, new level, and remaining attribute points is
returned.

If there are not enough attribute points, this command returns an EEXEC
error (0x08).

If the password is not accepted, this command fails without consequence.

**Params:**

- `pw` (Number) 32-bit password
- `id` (Number) which attribute to level up
- `callback` (Function) function to be triggered with response

### getPasswordSeed(callback : Function)

The Get Password Seed command returns Sphero's password seed.

Protected Sphero commands require a password.

Refer to the Sphero API documentation, Appendix D for more information.

**Params:**

- `callback` (Function) function to be triggered with response

### enableSSBAsyncMsg(flag : Number, callback : Function)

The Enable SSB Async Messages command turns on/off soul block related
asynchronous messages.

These include shield collision/regrowth messages, boost use/regrowth
messages, XP growth, and level-up messages.

This feature defaults to off.

**Params:**

- `flag` (Number) whether or not to enable async messages
- `callback` (Function) function to be triggered after write

### runMacro(id : Number, callback : Function)

The Run Macro command attempts to execute the specified macro.

Macro IDs are split into groups:

0-31 are System Macros. They are compiled into the Main Application, and
cannot be deleted. They are always available to run.

32-253 are User Macros. They are downloaded and persistently stored, and
can be deleted in total.

255 is the Temporary Macro, a special user macro as it is held in RAM for
execution.

254 is also a special user macro, called the Stream Macro that doesn't
require this call to begin execution.

This command will fail if there is a currently executing macro, or the
specified ID code can't be found.

**Params:**

- `id` (Number) 8-bit Macro ID to run
- `callback` (Function) function to be triggered with response

### saveTempMacro(macro : Array, callback : Function)

The Save Temporary Macro stores the attached macro definition into the
temporary RAM buffer for later execution.

If this command is sent while a Temporary or Stream Macro is executing it
will be terminated so that its storage space can be overwritten. As with
all macros, the longest definition that can be sent is 254 bytes.

**Params:**

- `macro` (Array) array of bytes with the data to be written
- `callback` (Function) function to be triggered with response

### saveMacro(macro : Array, callback : Function)

Save macro

The Save Macro command stores the attached macro definition into the
persistent store for later execution. This command can be sent even if
other macros are executing.

You will receive a failure response if you attempt to send an ID number in
the System Macro range, 255 for the Temp Macro and ID of an existing user
macro in the storage block.

As with all macros, the longest definition that can be sent is 254 bytes.

**Params:**

- `macro` (Array) array of bytes with the data to be written
- `callback` (Function) function to be triggered with response

### reInitMacroExec(callback : Function)

The Reinit Macro Executive command terminates any running macro, and
reinitializes the macro system.

The table of any persistent user macros is cleared.

**Params:**

- `callback` (Function) function to be triggered with response

### abortMacro(callback : Function)

The Abort Macro command aborts any executing macro, and returns both it's
ID code and the command number currently in progress.

An exception is a System Macro executing with the UNKILLABLE flag set.

A returned ID code of 0x00 indicates that no macro was running, an ID code
of 0xFFFF as the CmdNum indicates the macro was unkillable.

**Params:**

- `callback` (Function) function to be triggered with response

### getMacroStatus(callback : Function)

The Get Macro Status command returns the ID code and command number of the
currently executing macro.

If no macro is running, the 0x00 is returned for the ID code, and the
command number is left over from the previous macro.

**Params:**

- `callback` (Function) function to be triggered with response

### setMacroParam(index : Number, val1 : Number, val2 : Number, callback : Function)

The Set Macro Parameter command allows system globals that influence
certain macro commands to be selectively altered from outside of the macro
system itself.

The values of Val1 and Val2 depend on the parameter index.

Possible indices:

- **00h** Assign System Delay 1: Val1 = MSB, Val2 = LSB
- **01h** Assign System Delay 2: Val1 = MSB, Val2 = LSB
- **02h** Assign System Speed 1: Val1 = speed, Val2 = 0 (ignored)
- **03h** Assign System Speed 2: Val1 = speed, Val2 = 0 (ignored)
- **04h** Assign System Loops: Val1 = loop count, Val2 = 0 (ignored)

For more details, please refer to the Sphero Macro document.

**Params:**

- `index` (Number) what parameter index to use
- `val1` (Number) value 1 to set
- `val2` (Number) value 2 to set
- `callback` (Function) function to be triggered with response

### appendMacroChunk(chunk : Array, callback : Function)

The Append Macro Chunk project stores the attached macro definition into
the temporary RAM buffer for later execution.

It's similar to the Save Temporary Macro command, but allows building up
longer temporary macros.

Any existing Macro ID can be sent through this command, and executed
through the Run Macro call using ID 0xFF.

If this command is sent while a Temporary or Stream Macro is executing it
will be terminated so that its storage space can be overwritten. As with
all macros, the longest chunk that can be sent is 254 bytes.

You must follow this with a Run Macro command (ID 0xFF) to actually get it
to go and it is best to prefix this command with an Abort call to make
certain the larger buffer is completely initialized.

**Params:**

- `chunk` (Array) macro chunk to write
- `callback` (Function) function to be triggered with response

### eraseOrbBasicStorage(area : Number, callback : Function)

The Erase orbBasic Storage command erases any existing program in the
specified storage area.

Specify 0x00 for the temporary RAM buffer, or 0x01 for the persistent
storage area.

**Params:**

- `area` (Number) which area to erase
- `callback` (Function) function to be triggered with response

### appendOrbBasicFragment(area : Number, code : String, callback : Function)

The Append orbBasic Fragment command appends a patch of orbBasic code to
existing ones in the specified storage area (0x00 for RAM, 0x01 for
persistent).

Complete lines are not required. A line begins with a decimal line number
followed by a space and is terminated with a <LF>.

See the orbBasic Interpreter document for complete information.

Possible error responses would be ORBOTIX_RSP_CODE_EPARAM if an illegal
storage area is specified or ORBOTIX_RSP_CODE_EEXEC if the specified
storage area is full.

**Params:**

- `area` (Number) which area to append the fragment to
- `code` (String) orbBasic code to append
- `callback` (Function) function to be triggered with response

### executeOrbBasicProgram(area : Number, slMSB : Number, slLSB : Number, callback : Function)

The Execute orbBasic Program command attempts to run a program in the
specified storage area, beginning at the specified line number.

This command will fail if there is already an orbBasic program running.

**Params:**

- `area` (Number) which area to run from
- `slMSB` (Number) start line
- `slLSB` (Number) start line
- `callback` (Function) function to be triggered with response

### abortOrbBasicProgram(callback : Function)

The Abort orbBasic Program command aborts execution of any currently
running orbBasic program.

**Params:**

- `callback` (Function) function to be triggered with response

### submitValueToInput(val : Number, callback : Function)

The Submit value To Input command takes the place of the typical user
console in orbBasic and allows a user to answer an input request.

If there is no pending input request when this API command is sent, the
supplied value is ignored without error.

Refer to the orbBasic language document for further information.

**Params:**

- `val` (Number) value to respond with
- `callback` (Function) function to be triggered with response

### commitToFlash(callback : Function)

The Commit To Flash command copies the current orbBasic RAM program to
persistent flash storage.

It will fail if a program is currently executing out of flash.

**Params:**

- `callback` (Function) function to be triggered with response