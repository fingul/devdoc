
--------------------------------

#일단 이슈 올려둠
https://github.com/oaubert/python-vlc/issues/16

# we need this : https://github.com/oaubert/python-vlc/issues/15 - Update PyPI package
# 안하면 osx에서 plugin 못찾는다고 나옴
pip install -e git+https://github.com/oaubert/python-vlc#egg=python-vlc


SOURCE = 'rtmp://192.168.0.51:1935/live/xxx'





SOURCE = "0.mp4"

SOURCE = '/Users/m/0.mp4'
import time
import vlc
vlc.libvlc_get_version()
Instance = vlc.Instance('--vout dummy --aout dummy')
player = Instance.media_player_new()
Media = Instance.media_new(SOURCE)
player.set_media(Media)
player.play()
player.get_state()

ms = vlc.MediaStats()
Media.get_stats(ms) and print(ms)
Media.parse()

#wait for media open 10 seconds / (also, can use event)
// for i in range(0,20):
//     if Media.is_parsed():
//         break
//     time.sleep(0.5)
Media.tracks_get()    

#안됨!!!! -> 되야함!!!
#Media.tracks_get()

--------------------------------
import vlc
import sys
import time

class vlc_instance(object):
    """create an instance of vlc-player
    """
    
    def __init__(self):
        self.title = None
        self.artist = None
        self.album = None
        self.tracknumber = None
        self.url = None
        self.nowplaying = None
        self.position = None
        self.old_position = None
        
        self.INSTANCE = vlc.Instance('')
        self.player = self.INSTANCE.media_player_new()
        self.media = self.INSTANCE.media_new('')
        
        self.events = vlc.EventType
        self.manager = self.player.event_manager()
        self.mediaManager = self.media.event_manager()

    def format_time(self, milliseconds):
        """formats milliseconds to h:mm:ss
        """
        self.position = milliseconds / 1000
        m, s = divmod(self.position, 60)
        h, m = divmod(m, 60)
        return "%d:%02d:%02d" % (h, m, s)

    def load_media(self, file):
        """loads a file or stream
        """
        self.media = self.INSTANCE.media_new(file)
        self.player.set_media(self.media)

        self.mediaManager = self.media.event_manager()
        self.mediaManager.event_attach(vlc.EventType.MediaParsedChanged,
                                      self.meta_callback, self.media)

        self.mediaManager.event_attach(vlc.EventType.MediaStateChanged,
                                  self.state_callback,self.player)

        self.player.play()


    def pos_callback(self, event, player):
        print(self.format_time(event.u.new_time))
        
    def state_callback(self,event,player):
        print(player.get_state())

    def meta_callback(self, event, media):
        self.title = media.get_meta(vlc.Meta.Title)
        self.artist = media.get_meta(vlc.Meta.Artist)
        self.album = media.get_meta(vlc.Meta.Album)
        self.tracknumber = media.get_meta(vlc.Meta.TrackNumber)
        self.url = media.get_meta(vlc.Meta.URL)
        self.nowplaying = media.get_meta(vlc.Meta.NowPlaying)
    
test = vlc_instance()

test.manager.event_attach(vlc.EventType.MediaPlayerTimeChanged,
                                  test.pos_callback,test.player)

test.load_media('rtmp://192.168.0.51:1935/live/xxx')
time.sleep(1000)

--------------------------------




# 여기만 어떻게 하면 될것 같은데 안되고 있음.
'''

import ctypes
from vlc import MediaTrack
p = ctypes.POINTER(MediaTrack)()



n = vlc.libvlc_media_tracks_get(Media, ctypes.byref(p))


p.contents

tracks = [p[i]for i in range(n)]
a = ctypes.byref(p[0])
a


info = ctypes.cast(p, ctypes.POINTER(ctypes.POINTER(MediaTrack) * n))

'''

import ctypes
from vlc import MediaTrack
p = ctypes.POINTER(MediaTrack)()

import time
time.sleep(1)

n = vlc.libvlc_media_tracks_get(Media,ctypes.byref(p))

info = ctypes.cast(p, ctypes.POINTER(ctypes.POINTER(MediaTrack) * n))


Out[12]: 2

In [13]: p
Out[13]: <vlc.LP_MediaTrack at 0x106c74510>



#/Users/m/Downloads/vlc-2.2.4/modules/control/rc.c@    



                static int updateStatistics( intf_thread_t *p_intf, input_item_t *p_item )
                {
                    if( !p_item ) return VLC_EGENERIC;

                    vlc_mutex_lock( &p_item->lock );
                    vlc_mutex_lock( &p_item->p_stats->lock );
                    msg_rc( "+----[ begin of statistical info ]" );

                    /* Input */
                    msg_rc("%s", _("+-[Incoming]"));
                    msg_rc(_("| input bytes read : %8.0f KiB"),
                            (float)(p_item->p_stats->i_read_bytes)/1024 );
                    msg_rc(_("| input bitrate    :   %6.0f kb/s"),
                            (float)(p_item->p_stats->f_input_bitrate)*8000 );
                    msg_rc(_("| demux bytes read : %8.0f KiB"),
                            (float)(p_item->p_stats->i_demux_read_bytes)/1024 );
                    msg_rc(_("| demux bitrate    :   %6.0f kb/s"),
                            (float)(p_item->p_stats->f_demux_bitrate)*8000 );
                    msg_rc(_("| demux corrupted  :    %5"PRIi64),
                            p_item->p_stats->i_demux_corrupted );
                    msg_rc(_("| discontinuities  :    %5"PRIi64),
                            p_item->p_stats->i_demux_discontinuity );
                    msg_rc("|");
                    /* Video */
                    msg_rc("%s", _("+-[Video Decoding]"));
                    msg_rc(_("| video decoded    :    %5"PRIi64),
                            p_item->p_stats->i_decoded_video );
                    msg_rc(_("| frames displayed :    %5"PRIi64),
                            p_item->p_stats->i_displayed_pictures );
                    msg_rc(_("| frames lost      :    %5"PRIi64),
                            p_item->p_stats->i_lost_pictures );
                    msg_rc("|");
                    /* Audio*/
                    msg_rc("%s", _("+-[Audio Decoding]"));
                    msg_rc(_("| audio decoded    :    %5"PRIi64),
                            p_item->p_stats->i_decoded_audio );
                    msg_rc(_("| buffers played   :    %5"PRIi64),
                            p_item->p_stats->i_played_abuffers );
                    msg_rc(_("| buffers lost     :    %5"PRIi64),
                            p_item->p_stats->i_lost_abuffers );
                    msg_rc("|");
                    /* Sout */
                    msg_rc("%s", _("+-[Streaming]"));
                    msg_rc(_("| packets sent     :    %5"PRIi64),
                        p_item->p_stats->i_sent_packets );
                    msg_rc(_("| bytes sent       : %8.0f KiB"),
                            (float)(p_item->p_stats->i_sent_bytes)/1024 );
                    msg_rc(_("| sending bitrate  :   %6.0f kb/s"),
                            (float)(p_item->p_stats->f_send_bitrate*8)*1000 );
                    msg_rc("|");
                    msg_rc( "+----[ end of statistical info ]" );
                    vlc_mutex_unlock( &p_item->p_stats->lock );
                    vlc_mutex_unlock( &p_item->lock );

                    return VLC_SUCCESS;
                }

# /Users/m/Downloads/vlc-2.2.4/src/input/es_out.c


    switch( fmt->i_cat )
    {
    case AUDIO_ES:
        info_category_AddInfo( p_cat, _("Type"), _("Audio") );

        if( fmt->audio.i_physical_channels )
            info_category_AddInfo( p_cat, _("Channels"), "%s",
                                   _( aout_FormatPrintChannels( &fmt->audio ) ) );

        if( fmt->audio.i_rate > 0 )
        {
            info_category_AddInfo( p_cat, _("Sample rate"), _("%u Hz"),
                                   fmt->audio.i_rate );
            /* FIXME that should be removed or improved ! (used by text/strings.c) */
            var_SetInteger( p_input, "sample-rate", fmt->audio.i_rate );
        }

        unsigned int i_bitspersample = fmt->audio.i_bitspersample;
        if( i_bitspersample <= 0 )
            i_bitspersample = aout_BitsPerSample( p_fmt_es->i_codec );
        if( i_bitspersample > 0 )
            info_category_AddInfo( p_cat, _("Bits per sample"), "%u",
                                   i_bitspersample );

        if( fmt->i_bitrate > 0 )
        {
            info_category_AddInfo( p_cat, _("Bitrate"), _("%u kb/s"),
                                   fmt->i_bitrate / 1000 );
            /* FIXME that should be removed or improved ! (used by text/strings.c) */
            var_SetInteger( p_input, "bit-rate", fmt->i_bitrate );
        }
        for( int i = 0; i < AUDIO_REPLAY_GAIN_MAX; i++ )
        {
            const audio_replay_gain_t *p_rg = &fmt->audio_replay_gain;
            if( !p_rg->pb_gain[i] )
                continue;
            const char *psz_name;
            if( i == AUDIO_REPLAY_GAIN_TRACK )
                psz_name = _("Track replay gain");
            else
                psz_name = _("Album replay gain");
            info_category_AddInfo( p_cat, psz_name, _("%.2f dB"),
                                   p_rg->pf_gain[i] );
        }
        break;

    case VIDEO_ES:
        info_category_AddInfo( p_cat, _("Type"), _("Video") );

        if( fmt->video.i_width > 0 && fmt->video.i_height > 0 )
            info_category_AddInfo( p_cat, _("Resolution"), "%ux%u",
                                   fmt->video.i_width, fmt->video.i_height );

        if( fmt->video.i_visible_width > 0 &&
            fmt->video.i_visible_height > 0 )
            info_category_AddInfo( p_cat, _("Display resolution"), "%ux%u",
                                   fmt->video.i_visible_width,
                                   fmt->video.i_visible_height);
       if( fmt->video.i_frame_rate > 0 &&
           fmt->video.i_frame_rate_base > 0 )
       {
           div = lldiv( (float)fmt->video.i_frame_rate /
                               fmt->video.i_frame_rate_base * 1000000,
                               1000000 );
           if( div.rem > 0 )
               info_category_AddInfo( p_cat, _("Frame rate"), "%"PRId64".%06u",
                                      div.quot, (unsigned int )div.rem );
           else
               info_category_AddInfo( p_cat, _("Frame rate"), "%"PRId64,
                                      div.quot );
       }
       if( fmt->i_codec != p_fmt_es->i_codec )
       {
           const char *psz_chroma_description =
                vlc_fourcc_GetDescription( VIDEO_ES, fmt->i_codec );
           if( psz_chroma_description )
               info_category_AddInfo( p_cat, _("Decoded format"), "%s",
                                      psz_chroma_description );
       }

       break;

    case SPU_ES:
        info_category_AddInfo( p_cat, _("Type"), _("Subtitle") );
        break;

    default:
        break;
    }