---
title: Lecture
layout: default

DEFAULT_KALTURA_VIDEO_URL: "https://cdnapisec.kaltura.com/p/2640881/sp/264088100/embedIframeJs/uiconf_id/45517092/partner_id/2640881?iframeembed=true&playerId=kplayer&entry_id=ENTRYID&flashvars[streamerType]=auto"
DEFAULT_KALTURA_PLAYLIST_URL: "https://www.kaltura.com/p/2640881/sp/264088100/embedIframeJs/uiconf_id/44902351/partner_id/2640881/widget_id/0_dn12cuxd?iframeembed=true&playerId=kaltura_player_&flashvars[playlistAPI.kpl0Id]=PLAYLISTID&flashvars[ks]=&&flashvars[imageDefaultDuration]=30&flashvars[localizationCode]=en&flashvars[leadWithHTML5]=true&flashvars[forceMobileHTML5]=true&flashvars[nextPrevBtn.plugin]=true&flashvars[hotspots.plugin]=true&flashvars[sideBarContainer.plugin]=true&flashvars[sideBarContainer.position]=left&flashvars[sideBarContainer.clickToClose]=true&flashvars[chapters.plugin]=true&flashvars[chapters.layout]=vertical&flashvars[chapters.thumbnailRotator]=false&flashvars[streamSelector.plugin]=true&flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&flashvars[dualScreen.plugin]=true&flashvars[playlistAPI.playlistUrl]=https://kaf.berkeley.edu/playlist/details/{playlistAPI.kpl0Id}/categoryid/175896392"
---

# Lecture Viewer

<noscript>JavaScript must be enabled to view the requested video!</noscript>
<div id="load_msg" style="align:center;"></div>
<!-- <iframe id="video_viewer" src="" width="100%" height="750px" style="display:none;"></iframe> -->
<iframe id="kaltura_video_viewer" src="" width="100%" height="750px" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" style="display:none;"></iframe>
<iframe id="drive_viewer" src="" style="width:100%; height:750px; border:0;display:none;background-color:white;" allow="autoplay *; fullscreen *; encrypted-media *" sandbox="allow-same-origin allow-scripts allow-popups allow-forms"></iframe>
<iframe id="ytpl_viewer" width="100%" height="750px" src="" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<script>function main() {
    var default_drive_url = "https://drive.google.com/embeddedfolderview?id=FID#list"
    var default_drive_file_url = "https://drive.google.com/file/d/VID/preview"
    var default_yt_playlist_url = "https://www.youtube.com/embed/videoseries?list="
    var default_yt_video_url = "https://www.youtube.com/embed/"
    var default_kaltura_video_url = "{{page.DEFAULT_KALTURA_VIDEO_URL}}";
    var default_kaltura_playlist_url = "{{page.DEFAULT_KALTURA_PLAYLIST_URL}}";
    var kaltura_video_id_param = "kaltura_video_id";
    var kaltura_playlist_id_param = "kaltura_playlist_id";
    var gdrive_id_param = "gfid";
    var gdrive_video_id_param = "gvid";
    var yt_playlist_id_param = "ytplid";
    var yt_video_id_param = "ytvid";
    var kaltura_iframe = document.getElementById('kaltura_video_viewer');
    var drive_iframe = document.getElementById('drive_viewer');
    var ytpl_iframe = document.getElementById('ytpl_viewer');
    var msg = document.getElementById('load_msg');
    msg.innerText = "Loading the video...";
    function getUrlVars() {
        var vars = {};
        var parts = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m,key,value) {
            vars[key] = value;
        });
        return vars;
    }
    function getUrlParam(parameter, defaultvalue){
        var urlparameter = defaultvalue;
        if(window.location.href.indexOf(parameter) > -1){
            urlparameter = getUrlVars()[parameter];
            }
        return urlparameter;
    }
    var kaltura_video = getUrlParam(kaltura_video_id_param);
    var kaltura_playlist = getUrlParam(kaltura_playlist_id_param);
    var gf = getUrlParam(gdrive_id_param);
    var gv = getUrlParam(gdrive_video_id_param);
    var ytv = getUrlParam(yt_video_id_param);
    var ytp = getUrlParam(yt_playlist_id_param);
    // if (video == undefined) {
    //     video = window.location.pathname.replace(RegExp("^" + this_base_url + "/?"), "");
    // }
    if ((kaltura_video == undefined || kaltura_video == "") && 
    (kaltura_playlist == undefined || kaltura_playlist == "") && 
    (gf == undefined || gf == "") && 
    (gv == undefined || gv == "") && 
    (ytv == undefined || ytv == "") && 
    (ytp == undefined || ytp == "")) {
        msg.innerText = "Could not find a requested video!";
    } else {
        if (!(ytv == undefined || ytv == "")) {
            video_url = default_yt_video_url + ytv
            msg.innerHTML = "You must be logged into your Berkeley account to view this video. If you are having trouble view the video, please use the <a href='https://www.youtube.com/watch?v=" + ytv + "'>direct link</a>";
            ytpl_iframe.src = video_url;
            ytpl_iframe.style.display = "block";
            return;
        } else if (!(ytp == undefined || ytp == "")) {
            video_url = default_yt_playlist_url + ytp
            msg.innerHTML = "You must be logged into your Berkeley account to view this video. If you are having trouble view the video, please use the <a href='https://www.youtube.com/playlist?list=" + ytp + "'>direct link</a>";
            ytpl_iframe.src = video_url;
            ytpl_iframe.style.display = "block";
            return;
        } else if (!(gv == undefined || gv == "")) {
            video_url = default_drive_file_url.replace("VID", gv);
            msg.style.display = "none";
            drive_iframe.src = video_url;
            drive_iframe.style.display = "block";
            return;
        } else if (!(gf == undefined || gf == "")) {
            video_url = default_drive_url.replace("FID", gf);
            msg.innerHTML = "<a target='_blank' href='https://drive.google.com/drive/folders/" + gf + "?usp=sharing'>Direct Link</a> (Please use if your default Google account is not your Berkeley account.)<br>DO NOT REQUEST ACCESS as we will not grant non-Berkeley accounts to view the content.<br>"
            drive_iframe.src = video_url;
            drive_iframe.style.display = "block";
            return;
        } else if (!(kaltura_playlist == undefined || kaltura_playlist == "")) {
            video_url = default_kaltura_playlist_url.replace("PLAYLISTID", kaltura_playlist);
        } else {
            video_url = default_kaltura_video_url.replace("ENTRYID", kaltura_video);
        }
        msg.style.display = "none";
        kaltura_iframe.src = video_url;
        kaltura_iframe.style.display = "block";
    }
}
main();
</script>
