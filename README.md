A log of the difficulties we experience running the [pixelated-user-agent](https://github.com/pixelated/pixelated-user-agent).

## Versions

* OSX 10.10.4
* Vagrant 1.7.4
* VirtualBox 4.3.26 r98988

## 5th September 2015

11- Seen on luigi's Mac: After Ctrl-C'ing the user agent and restarting, the web app would not load. Gets stuck on the loading screen with the flashing pixelated box and never progresses. Fixed by `vagrant halt`ing and `vagrant up`ping. We also saw this  at the last hack day.

12- `soledad.DuplicatedDocumentError`:
```
user-agent-venv)vagrant@leap-wheezy:/vagrant$ pixelated-user-agent --config /vagrant/pixelated.example -lc /vagrant/service/pixelated/certificates/dev.pixelated-project.org.ca.crt --host 0.0.0.0
2015-09-05 05:42:49 [twisted] INFO PixelatedSite starting on 3333
2015-09-05 05:42:49 [twisted] INFO Starting factory <pixelated.config.site.PixelatedSite instance at 0x3727680>
2015-09-05 05:42:49 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): dev.pixelated-project.org
2015-09-05 05:42:56 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): dev.pixelated-project.org
2015-09-05 05:42:57 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): dev.pixelated-project.org
2015-09-05 05:42:59 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): api.dev.pixelated-project.org
2015-09-05 05:43:01 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): api.dev.pixelated-project.org
2015-09-05 05:43:03 [leap.soledad.client.secrets] INFO Checking if there's a secret in local storage...
2015-09-05 05:43:03 [leap.soledad.client.secrets] INFO Found a secret in local storage.
2015-09-05 05:43:03 [twisted] INFO Mail post-sync hook: processing queued docs
2015-09-05 05:43:03 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): api.dev.pixelated-project.org
2015-09-05 05:43:05 [twisted] INFO Starting factory <leap.common.http._HTTP11ClientFactory instance at 0x3736ea8>
2015-09-05 05:43:07 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): api.dev.pixelated-project.org
2015-09-05 05:43:09 [twisted] ERROR Traceback (most recent call last):
2015-09-05 05:43:09 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 393, in callback
2015-09-05 05:43:09 [twisted] ERROR     self._startRunCallbacks(result)
2015-09-05 05:43:09 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 501, in _startRunCallbacks
2015-09-05 05:43:09 [twisted] ERROR     self._runCallbacks()
2015-09-05 05:43:09 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 588, in _runCallbacks
2015-09-05 05:43:09 [twisted] ERROR     current.result = callback(current.result, *args, **kw)
2015-09-05 05:43:09 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 1184, in gotResult
2015-09-05 05:43:09 [twisted] ERROR     _inlineCallbacks(r, g, deferred)
2015-09-05 05:43:09 [twisted] ERROR --- <exception caught here> ---
2015-09-05 05:43:09 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 1126, in _inlineCallbacks
2015-09-05 05:43:09 [twisted] ERROR     result = result.throwExceptionIntoGenerator(g)
2015-09-05 05:43:09 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/python/failure.py", line 389, in throwExceptionIntoGenerator
2015-09-05 05:43:09 [twisted] ERROR     return g.throw(self.type, self.value, self.tb)
2015-09-05 05:43:09 [twisted] ERROR   File "/vagrant/service/pixelated/bitmask_libraries/session.py", line 167, in _create_incoming_mail_fetcher
2015-09-05 05:43:09 [twisted] ERROR     inbox = yield account.callWhenReady(lambda _: account.getMailbox('INBOX'))
2015-09-05 05:43:09 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 588, in _runCallbacks
2015-09-05 05:43:09 [twisted] ERROR     current.result = callback(current.result, *args, **kw)
2015-09-05 05:43:09 [twisted] ERROR   File "/home/vagrant/user-agent-venv/src/leap.mail/src/leap/mail/adaptors/soledad.py", line 269, in get_first_doc_if_any
2015-09-05 05:43:09 [twisted] ERROR     raise DuplicatedDocumentError
2015-09-05 05:43:09 [twisted] ERROR leap.mail.adaptors.soledad.DuplicatedDocumentError:
2015-09-05 05:43:09 [twisted] INFO Stopping factory <leap.common.http._HTTP11ClientFactory instance at 0x3736ea8>
2015-09-05 05:43:09 [twisted] INFO (TCP Port 3333 Closed)
2015-09-05 05:43:09 [twisted] INFO Stopping factory <pixelated.config.site.PixelatedSite instance at 0x3727680>
2015-09-05 05:43:09 [twisted] INFO Main loop terminated.
```

13- I still get disconnected from `vagrant ssh` every so often (also seen 21st August -- issue 3).
```
(user-agent-venv)vagrant@leap-wheezy:/vagrant$ Connection to 127.0.0.1 closed by remote host.
Connection to 127.0.0.1 closed.
```

## 22nd August 2015

6- For every email address I enter when composing, I see the following error and the padlock next to the address on the UI is orange.
```
2015-08-21 01:51:06 [leap.keymanager] WARNING HTTP error retrieving key: HTTPError('403 Client Error: ...',)
2015-08-21 01:51:06 [leap.keymanager] WARNING Could net fetch keyinfo.
```

7- Val: The Pixelated UI gets stuck at 'Loading...'. No obvious errors in the log and no failed network requests. Restarting the user-agent doesn't help. Firefox/Ubuntu.

8- https://github.com/rdoh/pixelated-user-agent/blob/master/doc/first-steps.md references a 'hack day' vagrant VM. Does this exist?

9- Is there a public pixelated-platform somewhere (or one that could be used for a hack day) that allows receiving of mail? Does it not work on dev.p-p and try.p-p only because of the lack of MX records)?
  * seems to work on dev.p-p now (5th September 2015)

10- Is it possible to run a pixelated-platform on an EC2 instance or another VM?


## 21st August 2015

1- `/vagrant/service/development_requirements.txt` can't be parsed by the version of pip on the VM. Fixed in [pull request #436](https://github.com/pixelated/pixelated-user-agent/pull/436).

2- `dev.pixelated-project.org` stopped accepting sign-ups at around 10:00-10:30 (UTC+10) after 3 of us signed up (then giving `405 Method Not Allowed`). Tried a different IP with no luck. Mysteriously started working again around 12:25.
  * From @bwagnerr: "This is probably related to https://leap.se/code/issues/6570. The leap web app runs with apache and sometimes answers method not allowed. There are a lot of rules there and we didn't really had time to look at that and find out the root of the problem unfortunately."

3- I get disconnected from `vagrant ssh` every so often and the user-agent dies.

4- Then user-agent wouldn’t start (after vagrant disconnected) -- error below. @elimydlarz and I have seen this 3-4 times today and only been able to fix by `vagrant destroy`ing and re-`up`ping.
  * In Eli's case, this also broke the tests (`pep8` not existing) but not in mine.
  * Seems the key data for the account specified has been borked somehow. @fbernitt suggested trying with another pixelated-platform account, which worked for me. Not sure how/why this would happen.
```
(user-agent-venv)vagrant@leap-wheezy:/vagrant$ pixelated-user-agent --host 0.0.0.0 -lc /vagrant/service/pixelated/certificates/dev.pixelated-project.org.ca.crt
2015-08-20 01:36:21 [twisted] INFO Site starting on 3333
2015-08-20 01:36:21 [twisted] INFO Starting factory <twisted.web.server.Site instance at 0x3b08488>
Which provider do you want to connect to:
dev.pixelated-project.org
What's your username registered on the provider:
robin
Type your password:

2015-08-20 01:36:35 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): dev.pixelated-project.org
2015-08-20 01:36:44 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): dev.pixelated-project.org
2015-08-20 01:36:50 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): dev.pixelated-project.org
2015-08-20 01:36:53 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): api.dev.pixelated-project.org
2015-08-20 01:36:57 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): api.dev.pixelated-project.org
2015-08-20 01:37:00 [leap.soledad.client.secrets] INFO Checking if there's a secret in local storage...
2015-08-20 01:37:00 [leap.soledad.client.secrets] INFO Found a secret in local storage.
2015-08-20 01:37:00 [twisted] INFO Mail post-sync hook: processing queued docs
2015-08-20 01:37:00 [requests.packages.urllib3.connectionpool] INFO Starting new HTTPS connection (1): api.dev.pixelated-project.org
2015-08-20 01:37:02 [twisted] INFO Starting factory <leap.common.http._HTTP11ClientFactory instance at 0x3b17248>
2015-08-20 01:37:05 [leap.common.check] ERROR Bug: Wrong address in key data.
2015-08-20 01:37:05 [leap.common.check] ERROR   File "/home/vagrant/user-agent-venv/bin/pixelated-user-agent", line 9, in <module>
2015-08-20 01:37:05 [leap.common.check] ERROR     load_entry_point('pixelated-user-agent==0.1', 'console_scripts', 'pixelated-user-agent')()
2015-08-20 01:37:05 [leap.common.check] ERROR   File "/vagrant/service/pixelated/application.py", line 100, in initialize
2015-08-20 01:37:05 [leap.common.check] ERROR     reactor.run()
2015-08-20 01:37:05 [leap.common.check] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/base.py", line 1194, in run
2015-08-20 01:37:05 [leap.common.check] ERROR     self.mainLoop()
2015-08-20 01:37:05 [leap.common.check] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/base.py", line 1203, in mainLoop
2015-08-20 01:37:05 [leap.common.check] ERROR     self.runUntilCurrent()
2015-08-20 01:37:05 [leap.common.check] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/base.py", line 798, in runUntilCurrent
2015-08-20 01:37:05 [leap.common.check] ERROR     f(*a, **kw)
2015-08-20 01:37:05 [leap.common.check] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 393, in callback
2015-08-20 01:37:05 [leap.common.check] ERROR     self._startRunCallbacks(result)
2015-08-20 01:37:05 [leap.common.check] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 501, in _startRunCallbacks
2015-08-20 01:37:05 [leap.common.check] ERROR     self._runCallbacks()
2015-08-20 01:37:05 [leap.common.check] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 588, in _runCallbacks
2015-08-20 01:37:05 [leap.common.check] ERROR     current.result = callback(current.result, *args, **kw)
2015-08-20 01:37:05 [leap.common.check] ERROR   File "/home/vagrant/user-agent-venv/src/leap.keymanager/src/leap/keymanager/openpgp.py", line 323, in build_key
2015-08-20 01:37:05 [leap.common.check] ERROR     'Wrong address in key data.')
2015-08-20 01:37:05 [twisted] ERROR Traceback (most recent call last):
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 434, in errback
2015-08-20 01:37:05 [twisted] ERROR     self._startRunCallbacks(fail)
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 501, in _startRunCallbacks
2015-08-20 01:37:05 [twisted] ERROR     self._runCallbacks()
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 588, in _runCallbacks
2015-08-20 01:37:05 [twisted] ERROR     current.result = callback(current.result, *args, **kw)
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 1184, in gotResult
2015-08-20 01:37:05 [twisted] ERROR     _inlineCallbacks(r, g, deferred)
2015-08-20 01:37:05 [twisted] ERROR --- <exception caught here> ---
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 1126, in _inlineCallbacks
2015-08-20 01:37:05 [twisted] ERROR     result = result.throwExceptionIntoGenerator(g)
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/python/failure.py", line 389, in throwExceptionIntoGenerator
2015-08-20 01:37:05 [twisted] ERROR     return g.throw(self.type, self.value, self.tb)
2015-08-20 01:37:05 [twisted] ERROR   File "/vagrant/service/pixelated/config/leap.py", line 27, in initialize_leap
2015-08-20 01:37:05 [twisted] ERROR     yield leap_session.initial_sync()
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 1126, in _inlineCallbacks
2015-08-20 01:37:05 [twisted] ERROR     result = result.throwExceptionIntoGenerator(g)
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/python/failure.py", line 389, in throwExceptionIntoGenerator
2015-08-20 01:37:05 [twisted] ERROR     return g.throw(self.type, self.value, self.tb)
2015-08-20 01:37:05 [twisted] ERROR   File "/vagrant/service/pixelated/bitmask_libraries/session.py", line 72, in initial_sync
2015-08-20 01:37:05 [twisted] ERROR     yield self.nicknym.generate_openpgp_key()
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 1126, in _inlineCallbacks
2015-08-20 01:37:05 [twisted] ERROR     result = result.throwExceptionIntoGenerator(g)
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/python/failure.py", line 389, in throwExceptionIntoGenerator
2015-08-20 01:37:05 [twisted] ERROR     return g.throw(self.type, self.value, self.tb)
2015-08-20 01:37:05 [twisted] ERROR   File "/vagrant/service/pixelated/bitmask_libraries/nicknym.py", line 38, in generate_openpgp_key
2015-08-20 01:37:05 [twisted] ERROR     yield self._send_key_to_leap()
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/local/lib/python2.7/site-packages/twisted/internet/defer.py", line 588, in _runCallbacks
2015-08-20 01:37:05 [twisted] ERROR     current.result = callback(current.result, *args, **kw)
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/src/leap.keymanager/src/leap/keymanager/openpgp.py", line 323, in build_key
2015-08-20 01:37:05 [twisted] ERROR     'Wrong address in key data.')
2015-08-20 01:37:05 [twisted] ERROR   File "/home/vagrant/user-agent-venv/src/leap.common/src/leap/common/check.py", line 48, in leap_assert
2015-08-20 01:37:05 [twisted] ERROR     assert condition, message
2015-08-20 01:37:05 [twisted] ERROR exceptions.AssertionError: Wrong address in key data.
2015-08-20 01:37:05 [twisted] INFO (TCP Port 3333 Closed)
2015-08-20 01:37:05 [twisted] INFO Stopping factory <twisted.web.server.Site instance at 0x3b08488>
2015-08-20 01:37:05 [twisted] INFO Stopping factory <leap.common.http._HTTP11ClientFactory instance at 0x3b17248>
2015-08-20 01:37:05 [twisted] INFO Main loop terminated.
(user-agent-venv)vagrant@leap-wheezy:/vagrant$
```

5- I then got into a state where, even after `vagrant destroy`, `vagrant up` always got stuck at the following line. This only happened to me. There were no vagrant processes running but rebooting OSX fixed this problem.
```
==> source: Clearing any previously set forwarded ports...
```
