# solame

Python 3 wrapper for LAME Encoder library.  Written for a project using a Raspberry Pi.

I needed a Python 3 interface to the LAME encorder library; http://lame.sourceforge.net/ that worked on a Raspberry Pi.  I couldn't find one so I wrote my own using Python's built in Ctypes library.  It's a mono encoder because my need was a single-pass conference room recorder that created small files.

## Notes for Raspian

The Lame library should be installed with: 

    Using ~2,477 kB:

        sudo apt install lame 
        
    Or using ~1,063 kB:

        sudo apt install libmp3lame-dev

    Or using ~ 478 kB:

        sudo apt install libmp3lame0


## Pseudocode 

```Python
import solame as lame

# Set our encoding parameters
lame.set_sample_rate(44100) # This is the rate of the the INPUT pcm.
lame.set_num_channels(1)    # This is the number of channels of the INPUT pcm data.
lame.set_mode(lame.MONO)
lame.set_bit_rate(32)       # In Kbps. This setting overrides just about all others in LAME.  
lame.init_parameters()      # Never skip this.  Lame has default settings but this call is still mandatory.

while RECORDING_STATE:

  # Grab some PCM data from the input device
  pcm = SOME_KIND_OF_WAV_CAPTURE_FUNTCION()
  mp3_data = lame.encode_buffer(pcm)
  mp3file.write(mp3_data)

# Finish the MP3 encoding
mp3_data = lame.encode_flush()
mp3file.write(mp3_data)
 
```

## Contact

    import codecs; codecs.encode('wvzfgbepu@tznvy.pbz', 'rot13')
