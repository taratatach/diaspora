TODO:
1. re add airbrake
2. re add newrelic
3. fix asset_sync

#Resque.workers.each {|w| w.unregister_worker}

#how I deploy jd.com to heroku
git pull
git checkout joindiapsora
git rebase TAGNUMBER
bundle

git add .

git commit -am 'updating gemfile.lock'

steps:

1. heroku maintenance:on -a diaspora-production
2. make sure all resque jobs are done.

3. heroku scale slow_worker=0 super_slow_worker=0 catchall_worker=0 priority_worker=0


4. add sidekiq config
heroku config:add SIDEKIQ_CONCURRENCY=2  SIDEKIQ_RETRY=3 -a diaspora-production


git push heroku joindiaspora:master -f
5. heroku run rake db:migrate -a diaspora-production




heroku run rake db:migrate
heroku run 'rails runner "AssetSync.sync"' && heroku restart && heroku maintenance:off -a diaspora-production

heroku maintenance:off -a diaspora-production


kill heroku old cron jobs

