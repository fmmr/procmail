## procmail setup for Fredrik Rødland
This procmail-file originates from NTH (AKA NTNU) from 1995.  It has been tweeked on for a number of years in it's original shape & form. Then one day in november of 2001 I decided to take the step a bit further, and  completely re-wrote the file, while keeping most of the rules' functionality intact.

Thanks a lot to TIMO'S PROCMAIL TIPS on http://www.uwasa.fi/~ts/info/proctips.html

Valuable resources also on the following pages:
* http://handsonhowto.com/pmail102.html
* http://pm-doc.sourceforge.net/pm-tips.html
* http://angel.net/~nic/spam-x/
* http://agriroot.aua.gr/~nikant/nkvir-rc

### Version history: (current version on top)
* v6.00	130913	checked into github
* v5.00	080313	splitted maillists and tagged with destination folder to/on outlook@rodland
* v4.50	0801	Added spambayes server-side check
* v4.00	060418	Lots of changes since last-time.  time to re-version    
* v3.20	041105	added mailer@rodland.no to track those. added recipes-set 004 (AS). changed hostname to mail@rodland Added all files to CVS. General clean-up Commented out 035 - rec should be moved to 010 or 070
* v3.11	040414	clean-up of CAR/Stocklink news mails
* v3.10	031108	clean-up of numbering, comments, sorting, etc added quite a few lines to 010.05 (blacklist)
* v3.00	0309	ahs-mails goes to ahs@rodland.no, maillists goes to outlook@rodland.no.  Now I can controll which mails to pop.  ahs@rodland.no defines it's own procmail-rules to distinguish mails that should be popped or not.
* v2.60	030226	Lots of editing and bugfixing added variable to run anti-spam tests
* v2.52	030128	removed put_default-rule
* v2.51 030124	splitted more and started commenting
* v2.50 030123	splitted .procmailrc in multiple files added YAVR, cleaned up 00 (preprocess) rules (from 13 to 8)
* v2.06 030122	fixed some bugs, samundet now to outlook
* v2.05 030120	added lockfile-flag on all folder-recepies.
* v2.04	030117	changed impl of viewing mails.  now sending original
* v2.03	030116	changed listing of spam (both as cron or as sending list-mails)
* v2.02	030109	When a user verifies his/hers email an email is sent cleaned up variabÅÅÅÅ¯les, changed to trusted address in Anti-spam.  added some flags to control flow more easy.
* v2.01	030108	Tweaked and tuned anti-spam rules - seems like it's working
* v2.0	030106	Started modified Nic Wolfe's anti-span recepie. Added logging on which rule is hit to from-file. Added boolean FRAFMR to put mails from me in frafmr. Cleaned up some comments.  More mails to outlook. Added looping on forwarding to mobil
* v1.32	020808	Tuned vacationmails & subject/body I don't want to read (which are not to ME)
* v1.31	020806	Finished commenting - added a few small rules
* v1.30	020727	no new rules, but restructured and re-commented, and re-numbered all rules - not finished (must take rules 10-12 antoher time)
* v1.23	020705	added tradestats-rules
* v1.22	020604	(finally!) added klez-virus-rule
* v1.21	020502	moved out of 01.04 and added 11.01 (blacklisted domains)
* v1.20	020423	added razor as rule 00.05
* v1.11	020227	splitted maillist in with/without backup cleaned up NMWL perfected backup
* v1.10 020225	added backup-functionallity in monthly folder documentation fo rules need to be revised
* v1.06	0201	various addresses added to blacklisted sections
* v1.06	011129	re-structuring of 01-rules (with/out blacklisting etc)
* v1.05	0111	various small changes and additions to rules
* v1.04	011123	added a copy of 01.02 & 01.05 in blacklist
* v1.03	011122	Added rule 01.05
* v1.02	011121	added comments on to.  added ONLINE-var to avoid sending SMS when I'm ogged on
* v1.01	011120	re-write
* v0.2-v0.9	Many changes during the years
* v0.1	95	initial version

### ~/.procmailrc:
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

	should no longer use - if mails fall through they should be handled
	in 010 or 070
	INCLUDERC=$RECDIR/035_job.proc

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

### TODO-LIST
* 00.08 & 00.09 	cronjobs - samle dem under en og bytte 	overskrift på cronjobber og flytte 	ut av 00-reglene
* job: rule 09 & 13	here som vacation etc conditions which could be removed earlier
* div			add boolean on logging entering file
* div			add boolean on logging rule
* div			cell phone nmb should be made a variable
* pre 02		fix options to AS-listing
* pre 09 & 10		move to yavr