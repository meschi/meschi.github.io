---
layout: post
category: Audio
date: 2021-10-22
---

Ich vergesse immer meine Konfiguration um das Native Instruments Audio 4 DJ Interface auf Linux zu betreiben.

Mit folgender `~/.asoundrc` funktioniert mein Setup:

	pcm.AUDIO4DJ-tweak {
	    type multi;
	    # bind hardware devices
	    slaves.a.pcm "hw:Audio4DJ,0,0";
	    slaves.a.channels 2;
	    slaves.b.pcm "hw:Audio4DJ,0,1";
	    slaves.b.channels 2;
	    # bind channels to virtual device;
	    bindings.0.slave a;
	    bindings.0.channel 0;
	    bindings.1.slave a;
	    bindings.1.channel 1;
	    bindings.2.slave b;
	    bindings.2.channel 0;
	    bindings.3.slave b;
	    bindings.3.channel 1;
	}
	
	# JACK will be unhappy if there is no mixer to talk to, so we set
	# this to card 0. This could be any device but 0 is easy. 
	#note that audio4dj is actually card 1 -- we are faking mixer elements so JACK is happy:
	
	ctl.AUDIO4DJ-tweak {
	        type hw;
	        card 0;
	}

