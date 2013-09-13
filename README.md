Fredriks procmail recipes

	#########################################################################
	# 									#
	#		PROCMAIL-FILE FOR FREDRIK M. RODLAND			#
	# 									#
	# This procmail-file originates from NTH (AKA NTNU) from 1995.  It has 	#
	# been tweeked on for a number of years in it's original shape & form.	#
	# Then one day in november of 2001 I decided to take the step a bit 	#
	# further, and  completely re-wrote the file, while keeping most of 	#
	# the rules' functionality intact.					#
	#									#
	# New things added are: scoring, variables, multi-line-rules, comments	#
	# on every single rule, use of ^TO/^TO_/^FROM_DAEMON, tweeking of PATH	#
	#									#
	# Thanks a lot to TIMO'S PROCMAIL TIPS on 				#
	# http://www.uwasa.fi/~ts/info/proctips.html				#
	#									#
	# Valuable resources also on the following pages:			#
	# http://handsonhowto.com/pmail102.html					#
	# http://pm-doc.sourceforge.net/pm-tips.html				#
	# http://angel.net/~nic/spam-x/						#
	# http://agriroot.aua.gr/~nikant/nkvir-rc				#
	#									#
	# Short rules description:						#
	# ========================						#
	# 000	Variables (Sets all variables used throughout the other files)	#
	# 003	Pre-processing rules				(nmb ok 031118)	#
	# 01		Tag source (NP)						#
	# 02		Backup (usually commented)				#
	# 03		RAZOR-check				(commented out)	#
	# 04		razor-mails => razor			(commented out)	#
	# 004	Anti-spam handling				(nmb ok 041105)	#
	# 01		List pending sender			(commented out)	#
	# 02		Accept someone				(commented out)	#
	# 03		View someone				(commented out)	#
	# 04		Deny someone				(commented out)	#
	# 05		change subject for spam-listing-mail			#
	# 06		Send matches from 05 to outlook				#
	# 07        	Block non-valid rodland-addresses (peter@rodland.no)	#
	# 08        	Block spam-domains (nate.com)				#
	# 09		Block spam-addresses (inet@microsoft.com)		#
	# 10		Block deny_deny (validated multiplt occurence spams)	#
	# 005	Yet another virus recipe			031118: v1.8.0	#
	# 010	Junk mails					(nmb ok 031118)	#
	# 01		No From, To and Subject					#
	# 02		Interscan messages                      		#
	# 03		Vacation mails (not to me) (commented out)		#
	# 04		FROM_DAEMON - split in to me & not to me		#
	# 05		mails to junk.*@rodland.no				#
	# 06		Bothersome meailaddresses				#
	# 035	Job-mails				(NOT IN USE - 041105)	#
	# 01		prod mail 						#
	# 02		pts-mail => keystone					#
	# 03 		tradestat 18:00						#
	# 04 		Dagsrapport						#
	# 05		Press releases						#
	# 06.a		CAR analyse mails					#
	# 06.b		Stocklink-daily-news-mails				#
	# 07		Stocklink-mails						#
	# 08		kursinfo => INNBOKS					#
	# 09		admin => ahs						#
	# 10		usa-orders => usa					#
	# 11		stocklink-dev & ahs-test => junk			#
	# 12		ahs-dev => ahs						#
	# 13		otc-stats => outlook					#
	# 14		OBI, OSE, VP => outlook					#
	# 15		bb.aston.no						#
	# 16		vakt-mails => ahs					#
	# 17		utv & aston => ahs			(nmb ok 031118)	#
	# 050	Various private							#
	# 01		mails from ME => frafmr					#
	# 02		mails from bank						#
	# 03		from kursinfo => kursinfo & fw omsatt-triggers to SMS	#
	# 04		Contract-notes from stocknet				#
	# 05		Alert messages from maisen (or a router)		#
	# 06		Cron mail to outlook					#
	# 070	Mailling lists					(nmb ok 031118)	#
	# 01		sit-pang & samfundet => outlook 			#
	# 02		skepsis => outlook					#
	# 03		music (police) => outlook				#
	# 04		nmwl in subject => outlook				#
	# 05		suse (on email) => suse					#
	# 06		subject [SLE] => suse					#
	# 07		to php => php						#
	# 08		subject [PHP] => php					#
	# 09		Morgenanalyse						#
	# 10		various to/from java => outlook				#
	# 11		resin => resin						#
	# 12		secrity => outlook					#
	# 13		procmail => outlook					#
	# 14		spambayes - list-id => outlook				#
	# 15		spambayes-dev - list-id => outlook			#
	# 16		spambayes-bugs - list-id => outlook			#
	# 17		spambayes - subject => outlook				#
	# 18		spambayes - from => outlook				#
	# 19		checkstyle - to => outlook				#
	# 20		checkstyle - subject => outlook				#
	# 21		Azureus                 				#
	# 22		CustomizeGoogle         				#
	# 23		razor => outlook					#
	# 24		subject [Razor-users]  => razorlist			#
	# 25		STOCKLINK daily-news mails          			#
	# 26		NN nyhetslarm						#
	# 27		various to/from => PCmailliste				#
	# 28		various to/from => outlook	WITH backup		#
	# 29		various to/from => outlook 	WITHOUT backup		#
	# 090	Post-processing					(nmb ok 031118)	#
	# 01		AS: Deny denied mails					#
	# 02		AS: has chicken						#
	# 03		AS: request chicken					#
	# 04		copy all mail to backup/innboks				#
	# 05		not to/cc/etc ME => INNBOKS (possibly junk)		#
	# 06		AS: Tag suspicious rodland - e.g. Xvcd@rodland.no	#
	# 07		AS: Unsure mail => unsure				#
	# 08		if excplicit to me (not cc) => copy to SMS		#
	# 									#
	# Version history: (current version on top)				#
	# v5.00	080313	splitted maillists and tagged with destination 		#
	#		folder to/on outlook@rodland				#
	# v4.50	0801	Added spambayes server-side check			#
	# v4.00	060418	Lots of changes since last-time.  time to re-version    #
	# v3.20	041105	added mailer@rodland.no to track those. added 		#
	#		recipes-set 004 (AS). changed hostname to mail@rodland	#
	#		Added all files to CVS. General clean-up		#
	#		Commented out 035 - rec should be moved to 010 or 070	#
	# v3.11	040414	clean-up of CAR/Stocklink news mails			#
	# v3.10	031108	clean-up of numbering, comments, sorting, etc		#
	#		added quite a few lines to 010.05 (blacklist)		#
	# v3.00	0309	ahs-mails goes to ahs@rodland.no, maillists goes to	#
	#		outlook@rodland.no.  Now I can controll which mails to	#
	#		pop.  ahs@rodland.no defines it's own procmail-rules	#
	#		to distinguish mails that should be popped or not	#
	# v2.60	030226	Lots of editing and bugfixing				#
	#		added variable to run anti-spam tests			#
	# v2.52	030128	removed put_default-rule				#
	# v2.51 030124	splitted more and started commenting			#
	# v2.50 030123	splitted .procmailrc in multiple files			#
	#		added YAVR, cleaned up 00 (preprocess) rules 		#
	#		(from 13 to 8)						#
	# v2.06 030122	fixed some bugs, samundet now to outlook		#
	# v2.05 030120	added lockfile-flag on all folder-recepies.		#
	# v2.04	030117	changed impl of viewing mails.  now sending original	#
	# v2.03	030116	changed listing of spam (both as cron or as sending	#
	#		list-mails)						#
	# v2.02	030109	When a user verifies his/hers email an email is sent	#
	#		cleaned up variabÅÅÅÅ¯les, changed to trusted	#
	#		address							#
	#		in Anti-spam.  added some flags to control flow more	#
	#		easy.							#
	# v2.01	030108	Tweaked and tuned anti-spam rules - seems like		#
	#		it's working						#
	# v2.0	030106	Started modified Nic Wolfe's anti-span recepie.		#
	#		Added logging on which rule is hit to from-file		#
	#		Added boolean FRAFMR to put mails from me in frafmr 	#
	#		Cleaned up some comments.  More mails to outlook.	#
	#		Added looping on forwarding to mobil			#
	# v1.32	020808	Tuned vacationmails & subject/body I don't want to 	#
	#		read (which are not to ME)				#
	# v1.31	020806	Finished commenting - added a few small rules		#
	# v1.30	020727	no new rules, but restructured and re-commented, 	#
	#		and re-numbered all rules - not finished 		#
	#		(must take rules 10-12 antoher time)			#
	# v1.23	020705	added tradestats-rules					#
	# v1.22	020604	(finally!) added klez-virus-rule			#
	# v1.21	020502	moved out of 01.04 and added 11.01			#
	#		(blacklisted domains)					#
	# v1.20	020423	added razor as rule 00.05				#
	# v1.11	020227	splitted maillist in with/without backup		#
	#		cleaned up NMWL						#
	#		perfected backup					#
	# v1.10 020225	added backup-functionallity in monthly folder		#
	#		documentation fo rules need to be revised		#
	# v1.06	0201	various addresses added to blacklisted sections		#
	# v1.06	011129	re-structuring of 01-rules (with/out blacklisting etc)	#
	# v1.05	0111	various small changes and additions to rules		#
	# v1.04	011123	added a copy of 01.02 & 01.05 in blacklist		#
	# v1.03	011122	Added rule 01.05					#
	# v1.02	011121	added comments on to.  added ONLINE-var to avoid 	#
	#		sending SMS when I'm ogged on				#
	# v1.01	011120	re-write						#
	# v0.2-v0.9	Many changes during the years				#
	# v0.1	95	initial version						#
	# 									#
	#########################################################################

	PROCDIR		= $HOME/procmail
	LOGFILE		= $PROCDIR/from
	RECDIR		= $PROCDIR/recipes

	MAILDIR         = $HOME/mail
	MONTH_FOLDER=../backup/old_mail/`date +%Y-%m`
	DUMMY=`test -d $MONTH_FOLDER || mkdir $MONTH_FOLDER`

	INCLUDERC=$RECDIR/000_variables.proc
	INCLUDERC=$RECDIR/003_preprocess.proc
	INCLUDERC=$RECDIR/004_anti_spam.proc
	INCLUDERC=$RECDIR/005_yavr.proc
	INCLUDERC=$RECDIR/010_junk.proc

	# should no longer use - if mails fall through they should be handled
	# in 010 or 070
	#INCLUDERC=$RECDIR/035_job.proc

	INCLUDERC=$RECDIR/050_fmr_main.proc
	INCLUDERC=$RECDIR/055_barn.proc
	INCLUDERC=$RECDIR/060_cron.proc
	INCLUDERC=$RECDIR/070_maillists_spec.proc
	INCLUDERC=$RECDIR/071_maillists_tech.proc
	INCLUDERC=$RECDIR/072_maillists_social.proc
	INCLUDERC=$RECDIR/073_maillists_finn.proc
	INCLUDERC=$RECDIR/074_maillists_bors.proc 
	INCLUDERC=$RECDIR/079_maillists.proc
	INCLUDERC=$RECDIR/090_postprocess.proc

	LOG = "** RULE: LAST RULE - INBOX $NL"

	#########################################################################
	# 									#
	#		TODO-LIST						#
	#									#
	#  00.08 & 00.09 	cronjobs - samle dem under en og bytte 		#
	#			overskrift pÅÅÅÂ cronjobber og flytte 	#
	#			ut av 00-reglene				#
	#  job: rule 09 & 13	here som vacation etc conditions which could 	#
	#			be removed earlier				#
	#  div			add boolean on logging entering file		#
	#  div			add boolean on logging rule			#
	#  div			cell phone nmb should be made a variable	#
	#  pre 02		fix options to AS-listing			#
	#  pre 09 & 10		move to yavr					#
	# 									#
	#########################################################################
