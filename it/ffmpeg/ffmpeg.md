# Learning Note of ffmpeg.
Source [ffmpeg documentation](https://ffmpeg.org/documentation.html)

ffmpeg actually is a suit of tools and libraries for working with media files. 

## Four command line tools
    ffmpeg : main tool 
    ffprobe: analysing tool
    ffplay : player
    ffserver: a media server
Each tool has two documents, the simple version and the "xxx-all" version.

## Components 
ffmpeg tools calls components API to do the job. On most of time, command line tool passes proper arguments to 
functions of these components based on tasks. For complicate tasks, user can transfer arguments to these components
directly. 

Following are components that has documents on the website
    Utilities
    Video scaling and pixel format converter
    Audio re-sampler
    Encoders and decoders (codecs)
    Bitstream filters
    Muxers and demuxers (formats)
    Protocols
    Input and output devices
    Filters

## Libraries 
Libraries are used by both tools and components. Ffmpeg documented following libraries
    libavutil
    libswscale
    libswresample
    libavcodec
    libavformat
    libavdevice
    libavfilter

## API 
Other than above user level documentation, ffmpeg also documented API for developers. These are in Doxygen format based on versions.

## Others
Among these useful documents officially provided by ffmpeg, there are General Documents that provide FAQ, External lib supporting misc and 
Community Contributed Documentation and a book.


This memory note will focus on Tools, Component and Library documents. 

# FFMPEG tool

## Synopsis

```ffmpeg [global options] {[input_file_options] -i input_url}... {[output_file_options] output_url}...```
    
5 sets of options shown on above synopsis syntax:
    1. Global options
    2. Input options
    3. Input media url
    4. Output options
    5. Output media url.

## Description
Ffmpeg composes output media files from a set of input files by perform various actions on input media files. 

### Concepts
    1. Media file 
    A media file contains 1 or more streams, or pictures. A stream contains audio or video data, multiple streams in a file are 
    aligned by media timeline. Stream is sometimes referred as tracks.

    2. Demux and Mux
    Streams from file comes with packed format. Demux splits streams, Mux assemble different streams back to file that align to the 
    timeline. 

    3. Referring : ```n:m```indicate the m-th stream in n-th file. Both n and m starts from 0. 

    4. -map option is used to refer the track in a stream. e.g: ```-map 1:2``` refers the 2nd file 3rd stream.

    5. Options are applied to next specified file. All options applies only to next file only and reset between files. So you must specify 
    options for each followed file.

## Detail Description
    Note: This is very important concept that must be remembered. With this concept in mind, you can then understand how ffmpeg various command 
    line options put together to perform the tasks.

    
     +-----------+  demuxer  +--------------------+  decoder    +---------------+
     |Input file | --------->| encoded data packet|  ---------> | decoded frames| --+
     +-----------+           +--------------------+             +---------------+   | encoder
                                                                                    |
                                                                                    |
                              +-------------+    muxer           +--------------+   |
                              |output file  | <----------------- |encoded frames|<--+
                              +-------------+                    +--------------+


    Ffmpeg put various filters to process the decoded frames before encoder.

### Filtering
Raw audio/video frames can be processed by filters. 
    
    1. Simple filtergraphs : one input and one output

    ``` -vf ``` video simple filter
    ``` -af ``` audio simple filter

    2. Complex filtergraphs : multiple inputs and outputs, not a linear filter at all.
    ``` -filter-complex```
           


