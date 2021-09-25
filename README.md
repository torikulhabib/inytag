# InyTag
TagLib For Valac

## Mp3, Mp4, Flac.
## APP used this libs.

    ## APP used this libs.
    
[![Get it on AppCenter](https://appcenter.elementary.io/badge.svg)](https://appcenter.elementary.io/com.github.torikulhabib.niki) 
[![Get it from the Snap Store](https://snapcraft.io/static/images/badges/en/snap-store-black.svg)](https://snapcraft.io/niki)

## You'll need the following dependencies:

* meson
* libtag1-dev

## Building
Run `meson` to configure the build environment and then `ninja` to build and run automated tests

    meson build --prefix=/usr
    cd build
    ninja

## Installation
To install, use `ninja install`

    sudo ninja install

## add Your messon build vala APP

    add_languages('cpp')

    meson.get_compiler('cpp').find_library('inytag', required : false),

## add FLATPAK .yaml

    - name: inytag
    buildsystem: meson
    sources:
      - type: git
        url: https://github.com/torikulhabib/inytag.git
        tag: master

## Testing
Example write with valac:

M4A Tag write:

    var file_mp4 = new InyTag.Mp4_File ("File Path");
    file_mp4.mp4_tag.title = "foo";
    file_mp4.mp4_tag.artist = "foo";
    file_mp4.mp4_tag.album = "foo";
    file_mp4.mp4_tag.genre = "foo";
    file_mp4.mp4_tag.comment = "foo";
    file_mp4.mp4_tag.year = (int) 2021;
    file_mp4.mp4_tag.track = (int) 0;
    InyTag.Mp4_Picture picture = new InyTag.Mp4_Picture ();
    picture.set_file (InyTag.Format_Type.JPEG, "image path");
    file_mp4.tag_mp4.set_item_picture (picture);
    file_mp4.save ();

Clear M4A Tag:

    var file_mp4 = new InyTag.Mp4_File ("File Path");
    file_mp4.mp4_tag.title = "";
    file_mp4.mp4_tag.artist = "";
    file_mp4.mp4_tag.album = "";
    file_mp4.mp4_tag.genre = "";
    file_mp4.mp4_tag.comment = "";
    file_mp4.mp4_tag.year = (int) 0;
    file_mp4.mp4_tag.track = (int) 0;
    file_mp4.remove_picture ();
    file_mp4.save ();

Read M4A Tag:

    var file_mp4 = new InyTag.Mp4_File ("File Path");
    string title = file_mp4.mp4_tag.title;
    string artist = file_mp4.mp4_tag.artist;
    string album = file_mp4.mp4_tag.album;
    string genre = file_mp4.mp4_tag.genre;
    string comment = file_mp4.mp4_tag.comment;
    int year = file_mp4.mp4_tag.year;
    int track = file_mp4.mp4_tag.track;
    int bitrate = file_mp4.audioproperties.bitrate;
    int samplerate = file_mp4.audioproperties.samplerate;
    int channel = file_mp4.audioproperties.channels;
    int lhenght = file_mp4.audioproperties.length;
    // Read Picture as gdkPixbuf
    InyTag.Mp4_Picture picture = file_mp4.tag_mp4.get_item_picture ();
    InyTag.ByteVector vector = picture.get_picture (InyTag.Format_Type.JPEG);
    Gdk.Pixbuf pixbuf = vector.get_pixbuf ();

FLAC Tag write:

    var file_flac = new InyTag.Flac_File ("File Path");
    file_flac.flac_tag.title = "foo";
    file_flac.flac_tag.artist = "foo";
    file_flac.flac_tag.album = "foo";
    file_flac.flac_tag.genre = "foo";
    file_flac.flac_tag.comment = "foo";
    file_flac.flac_tag.year = (int) 2021;
    file_flac.flac_tag.track = (int) 2;
    InyTag.Flac_Picture picture_flac = new InyTag.Flac_Picture ();
    picture_flac.mime_type = "mymetype";
    picture_flac.type = InyTag.Img_Type.FrontCover;
    picture_flac.set_picture ("Image Path");
    file_flac.add_picture (picture_flac);
    file_flac.save ();

Clear FLAC Tag :

    var file_flac = new InyTag.Flac_File ("File Path");
    file_flac.flac_tag.title = "";
    file_flac.flac_tag.artist = "";
    file_flac.flac_tag.album = "";
    file_flac.flac_tag.genre = "";
    file_flac.flac_tag.comment = "";
    file_flac.flac_tag.year = (int) 0;
    file_flac.flac_tag.track = (int) 0;
    //Choose option remove picture available all and part
    // remove all picture
    file_flac.remove_all_picture ();
    // remove picture in type
    file_flac.remove_picture (InyTag.Img_Type.FrontCover);
    // save tag
    file_flac.save ();

Read Flac tag :

    var file_flac = new InyTag.Flac_File ("file path");
    string title = file_flac.flac_tag.title;
    string artist = file_flac.flac_tag.artist;
    string album = file_flac.flac_tag.album;
    string genre = file_flac.flac_tag.genre;
    string comment = file_flac.flac_tag.comment;
    int year = (int) file_flac.flac_tag.year;
    int trck = (int) file_flac.flac_tag.track;
    int bitrate = file_flac.audioproperties.bitrate
    int sample rate = file_flac.audioproperties.samplerate;
    int channel = file_flac.audioproperties.channels;
    int lhtnght = file_flac.audioproperties.length;
    // read as GDK pixbuf
    InyTag.Flac_Picture picflac = file_flac.get_picture (InyTag.Img_Type.FrontCover);
    InyTag.ByteVector vector = picflac.get_picture ();
    var pixbuf = vector.get_pixbuf ();


MPEG Tag ID3V2 Write:

    var file_mpg = new InyTag.Mpeg_File ("file path");
    var frampic = new InyTag.ID3v2_Attached_Picture_Frame ();
    var framcomm = new InyTag.Attached_Comment_Frame ();
    file_mpg.id3v2_tag.add_text_frame (InyTag.Frame_ID.TITLE, "foo";);
    file_mpg.id3v2_tag.add_text_frame (InyTag.Frame_ID.LEADARTIST, "foo";);
    file_mpg.id3v2_tag.add_text_frame (InyTag.Frame_ID.ALBUM, "foo";);
    file_mpg.id3v2_tag.add_text_frame (InyTag.Frame_ID.CONTENTTYPE, "foo";);
    framcomm.set_encording (InyTag.String_Type.UTF16);
    framcomm.set_text ("foo";);
    file_mpg.id3v2_tag.add_comment_frame (framcomm);
    file_mpg.id3v2_tag.add_text_frame (InyTag.Frame_ID.TRACKNUM, "2021");
    file_mpg.id3v2_tag.add_text_frame (InyTag.Frame_ID.YEARV2, "2");
    frampic.mime_type = "Mymetype";
    frampic.type = InyTag.Img_Type.FrontCover;
    frampic.set_picture ("Image Path");
    file_mpg.id3v2_tag.add_picture_frame (frampic);
    file_mpg.save ();

Read MPEG Tag ID3V2;

    var file_mpg = new InyTag.Mpeg_File (File.new_for_uri ("file path");
    string title = file_mpg.id3v2_tag.get_text_frame (InyTag.Frame_ID.TITLE);
    string artist = file_mpg.id3v2_tag.get_text_frame (InyTag.Frame_ID.LEADARTIST);
    string album = file_mpg.id3v2_tag.get_text_frame (InyTag.Frame_ID.ALBUM);
    string genre = file_mpg.id3v2_tag.get_text_frame (InyTag.Frame_ID.CONTENTTYPE);
    string comment = file_mpg.id3v2_tag.get_text_frame (InyTag.Frame_ID.COMMENT);;
    int track = int.parse (file_mpg.id3v2_tag.get_text_frame (InyTag.Frame_ID.TRACKNUM));
    int year = int.parse (file_mpg.id3v2_tag.get_text_frame (InyTag.Frame_ID.YEARV2));
    int bitrate = file_mpg.audioproperties.bitrate;
    int samplerate = file_mpg.audioproperties.samplerate;
    int channel = file_mpg.audioproperties.channels;
    int lenght file_mpg.audioproperties.length;
    // Get picture as GDK pixbuf
    InyTag.ID3v2_Attached_Picture_Frame picture = file_mpg.id3v2_tag.get_picture_frame (InyTag.Img_Type.FrontCover);
    InyTag.ByteVector vector = picture.get_picture ();
    var pixbuf = vector.get_pixbuf ();

MPEG Tag ID3V1 Write:

    var file_mpg = new InyTag.Mpeg_File ("file payh");
    file_mpg.mpeg_tag.title = "foo";
    file_mpg.mpeg_tag.artist = "foo";
    file_mpg.mpeg_tag.album = "foo";
    file_mpg.mpeg_tag.genre = "foo";
    file_mpg.mpeg_tag.comment = "foo";
    file_mpg.mpeg_tag.year = 2021;
    file_mpg.mpeg_tag.track = 1;
    file_mpg.save ();

Read MPEG ID3V1:

    var file_mpg = new InyTag.Mpeg_File ("file payh");
    string title = file_mpg.mpeg_tag.title;
    string artist = file_mpg.mpeg_tag.artist;
    string album = file_mpg.mpeg_tag.album;
    string genre = file_mpg.mpeg_tag.genre;
    string comment = file_mpg.mpeg_tag.comment;
    int year = file_mpg.mpeg_tag.year;
    int treck = file_mpg.mpeg_tag.track;

MPEG CLEAR TAG ID3V2

    var file_mpg = new InyTag.Mpeg_File ("file path");
    file_mpg.id3v2_tag.remove_all ();
    file_mpg.save ();

MPEG Clear Tag ID3V1

    var file_mpg = new InyTag.Mpeg_File ("file path");
    file_mpg.mpeg_tag.title = "";
    file_mpg.mpeg_tag.artist ="";
    file_mpg.mpeg_tag.album = "";
    file_mpg.mpeg_tag.genre = "";
    file_mpg.mpeg_tag.comment = "";
    file_mpg.mpeg_tag.year = 0;
    file_mpg.mpeg_tag.track = 0;
    file_mpg.save ();

MPEG Clear ID3V1 And ID3V2

    var file_mpg = new InyTag.Mpeg_File ("file path");
    file_mpg.id3v2_tag.remove_all ();
    file_mpg.mpeg_tag.title = "";
    file_mpg.mpeg_tag.artist ="";
    file_mpg.mpeg_tag.album = "";
    file_mpg.mpeg_tag.genre = "";
    file_mpg.mpeg_tag.comment = "";
    file_mpg.mpeg_tag.year = 0;
    file_mpg.mpeg_tag.track = 0;
    file_mpg.save ();
