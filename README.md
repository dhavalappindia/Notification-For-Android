# Notification-For-Android


  int notifyID = 1;
        String CHANNEL_ID = "my_channel_01";
        NotificationManager notificationManager =
                (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
            CharSequence name = getString(R.string.app_name);// The user-visible name of the channel.
            int importance = NotificationManager.IMPORTANCE_HIGH;
            NotificationChannel mChannel = new NotificationChannel(CHANNEL_ID, name, importance);
            RemoteViews contentView = new RemoteViews
                    (getPackageName(), R.layout.design_notification);
            if (image != null)
                contentView.setImageViewBitmap(R.id.ivVideoThumb, image);
            contentView.setTextViewText(R.id.tvTitle, title);
            contentView.setTextViewText(R.id.tvDes, messageBody);

            Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
            NotificationCompat.Builder notificationBuilder = new NotificationCompat.Builder(this)
                    .setLargeIcon(BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher))
                    .setContentTitle(title)
                    .setSubText("")
                    .setContentText(messageBody)
                    .setAutoCancel(true)
                    .setSound(defaultSoundUri)
                    .setCustomBigContentView(contentView)
                    .setChannelId(CHANNEL_ID)
                    .setContentIntent(pendingIntent);

            notificationBuilder.setSmallIcon(R.drawable.ic_money_bag);

            notificationManager.createNotificationChannel(mChannel);

//            NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);

//            notificationManager.notify((int) System.currentTimeMillis() /* ID of notification */, notificationBuilder.build());
            notificationManager.notify(notifyID, notificationBuilder.build());

        } else {
            Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
            NotificationCompat.Builder notificationBuilder = new NotificationCompat.Builder(this)
                    .setLargeIcon(BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher))
                    .setContentTitle(title)
                    .setSubText("")
                    .setContentText(messageBody)
                    .setStyle(new NotificationCompat.BigPictureStyle()
                            .bigPicture(image))
                    .setAutoCancel(true)
                    .setSound(defaultSoundUri)
                    .setContentIntent(pendingIntent);

            notificationBuilder.setSmallIcon(R.mipmap.ic_launcher);

            notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);

//            notificationManager.notify((int) System.currentTimeMillis() /* ID of notification */, notificationBuilder.build());
            notificationManager.notify(notifyID, notificationBuilder.build());

        }
