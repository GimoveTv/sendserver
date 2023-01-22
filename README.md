# sendserver code

public class Main extends JavaPlugin {
	
	static Main instance;
	
	@Override
	public void onEnable() {
		instance = this;
		Bukkit.getMessenger().registerOutgoingPluginChannel(this, "BungeeCord");
	}
	public static void sendToServer(Player p, String server) {
		ByteArrayDataOutput out = ByteStreams.newDataOutput();
		out.writeUTF("Connect");
		out.writeUTF(server);
		p.sendPluginMessage(getInstance(), "BungeeCord", out.toByteArray());
	}
	
	public static Main getInstance() {
		return instance;
	}
	
	@Override
	public boolean onCommand(CommandSender sender, Command command, String label, String[] args) {
		if(command.getName().equalsIgnoreCase("hub")) {
			Player p = (Player) sender;
			if(args.length == 0) {
				sendToServer(p, "lobby");
			}
		}
		return true;
	}
}
