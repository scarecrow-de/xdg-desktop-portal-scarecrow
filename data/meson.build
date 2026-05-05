portal_dbus_interfaces = [
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Request.xml',
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Session.xml',
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.FileChooser.xml',
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Print.xml',
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Notification.xml',
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Inhibit.xml',
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Access.xml',
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Account.xml',
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Email.xml',
  desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.DynamicLauncher.xml',
]

fdo_dbus_interfaces = files(
  'org.freedesktop.ScreenSaver.xml',
  'org.freedesktop.Accounts.xml',
  'org.freedesktop.Accounts.User.xml',
)

gnome_dbus_interfaces = files(
  'io.github.scarecrow_de.SessionManager.xml',
  'io.github.scarecrow_de.ScreenSaver.xml',
)

gtk_portal = configuration_data()

if get_option('wallpaper').allowed()
  portal_dbus_interfaces += desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Wallpaper.xml'
  gtk_portal.set('wallpaper_iface', 'org.freedesktop.impl.portal.Wallpaper;')
else
  gtk_portal.set('wallpaper_iface', '')
endif

if get_option('settings').allowed()
  portal_dbus_interfaces += desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Settings.xml'
  gtk_portal.set('settings_iface', 'org.freedesktop.impl.portal.Settings;')
else
  gtk_portal.set('settings_iface', '')
endif

if get_option('appchooser').allowed()
  portal_dbus_interfaces += desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.AppChooser.xml'
  gtk_portal.set('appchooser_iface', 'org.freedesktop.impl.portal.AppChooser;')
else
  gtk_portal.set('appchooser_iface', '')
endif

if get_option('lockdown').allowed()
  portal_dbus_interfaces += desktop_portal_interfaces_dir / 'org.freedesktop.impl.portal.Lockdown.xml'
  gtk_portal.set('lockdown_iface', 'org.freedesktop.impl.portal.Lockdown;')
else
  gtk_portal.set('lockdown_iface', '')
endif

configure_file(
  input: 'scarecrow.portal.in',
  output: 'scarecrow.portal',
  configuration: gtk_portal,
  install: true,
  install_dir: datadir / 'xdg-desktop-portal/portals',
)

service_conf = configuration_data()
service_conf.set('libexecdir', libexecdir)
configure_file(
  input: 'org.freedesktop.impl.portal.desktop.scarecrow.service.in',
  output: 'org.freedesktop.impl.portal.desktop.scarecrow.service',
  configuration: service_conf,
  install: true,
  install_dir: dbus_service_dir,
)
configure_file(
  input: 'xdg-desktop-portal-scarecrow.service.in',
  output: 'xdg-desktop-portal-scarecrow.service',
  configuration: service_conf,
  install: true,
  install_dir: systemd_userunit_dir,
)

desktop_conf = configuration_data()
desktop_conf.set('libexecdir', libexecdir)
i18n.merge_file(
  type: 'desktop',
  input: configure_file(
    input: 'xdg-desktop-portal-scarecrow.desktop.in.in',
    output: 'xdg-desktop-portal-scarecrow.desktop.in',
    configuration: desktop_conf,
  ),
  output: 'xdg-desktop-portal-scarecrow.desktop',
  po_dir: '../po',
  install: true,
  install_dir: datadir / 'applications',
)
  
