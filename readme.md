# Jiggly quickstart guide

This document is intended to quickly get you up to speed on how Jiggly - the on-chain composer works with an example.

## Composer

To fully understand what you will eventually vote on, it is first best to get familiar with how compositions work.

### Step 1 - compositions

Grab yourself a composition from this [github](https://github.com/pret/pokered/blob/master/audio/music/celadon.asm) repository. (some are not compatible but the one linked should work fine).

Copy the contents of the file into your clipboard.

### Step 2 - play example

Open up [Jiggly](https://jiggly.app/#composer) and paste the clipboard contents into the composer. The composer immediately analyzes the composition and if it is valid it will tell you the exact number of segments required to compose the song. (in the case of the example song it should read 1109 segments)

Now you should be able to play the song.

*Note: Some of the commands are not relevant or are not supported. Refreshing the page after you've pasted the song will remove the unsupported commands and tidy up the composition.*

The on-chain composer produces a segment every 30 minutes therefore you can calculate the provisional composition time like this:

`1109 x 30 minutes = 33270 minutes = ~24 days`

### Step 3 - understanding the composer

Let's take a closer look at how you can achieve the desired composition.

The first line of the example song is (the channel definition does not matter as it is injected automatically)
```
  tempo 144	
```

The composer breaks up every line into 2 parts:
`_command_` and `[_parameters_]`, in this case, `tempo` and `[144]`.

Each command and individual parameter is decided by a segment. (The first desired segment option is `tempo` and the second one is `144`.)

### Step 4 - trade to compose 

Traders always vote on the outcome of the next segment and can observe the possible options in the app.

Here's a screenshot of how it works:

![Screenshot](https://github.com/JigglyTheDuck/docs/blob/master/screenshot.png)

In this example, if you are aiming to get `tempo` to be the next segment option but it currently only has 164 votes (as opposed to `duty_cycle` which has 953).

The command `tempo` will only be selected if it has the most votes at the end of the segment.

#### Influencing segment outcome

To make sure that `tempo` has the most votes you can sell 800 tokens at a registered liquidity pool like this:

 1. Check the decimal value of the option: `tempo` is `x.01`
 2. Click on `Trade` and sell 800.01 tokens.

This will add 800 votes to `tempo` and since 800 + 164 = 964 > 953, `tempo` now will become the leading candidate for the segment.

This process is repeated over and over until all 3 channels receive the `end_channel` command, at which point the composition is considered final.


