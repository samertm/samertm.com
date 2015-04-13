title: "fixing hugo"
date: 2014-04-27 07:00
---

I couldn't figure out how to have the chrome templates access data to see what page they're on, so I wrote this script to add the "active" class to an element.

    fix_css_has_run = false;
    function fix_css(){
        fix_css_has_run = true;
        var url_arr = document.URL.split("/");
        var li_id = "";
        var after_samertm = false;
        for (var i = 0; i < url_arr.length; i++) {
            if (after_samertm) {
                li_id = url_arr[i];
                break;
            } else {
                if (url_arr[i] === "samertm.com") {
                    after_samertm = true;
                }
            }
        }
        var elem = null;
        if (li_id == "") {
            elem = document.getElementById("home");
        } else {
            elem = document.getElementById(li_id);
        }
        elem.className = elem.className + " active";
    };
    
    document.addEventListener("DOMContentLoaded", fix_css, false);
    
    // if DOMContentLoaded does not exist
    window.onload = function() {
        if (!fix_css_has_run) {
	    fix_css();
        }
    };

Javascript saves the day once again!
