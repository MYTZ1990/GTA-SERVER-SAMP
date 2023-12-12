#include <a_samp>
#include <streamer>
#include <sscanf2>
#include <zcmd>
#include <a_mysql>

#define MYSQL_HOST "localhost"
#define MYSQL_USER "root"
#define MYSQL_PASSWORD ""
#define MYSQL_BASE_DE_DATOS "cuentas calles colombianas"



new NombreJugador[MAX_PLAYERS][MAX_PLAYER_NAME];
new MySQL:Database;

main()
{
	print("\n----------------------------------");
	print("  Bare Script\n");
	print("----------------------------------\n");
}

public OnPlayerConnect(playerid)
{
    GameTextForPlayer(playerid, "~w~SA-MP: ~r~Bare Script", 5000, 5);
    GetPlayerName(playerid, NombreJugador[playerid], MAX_PLAYER_NAME);

    new DB_Query[256];
    new Cache:ResultCache;

    mysql_format(Database, DB_Query, sizeof(DB_Query), "SELECT * FROM cuentas WHERE nombre='%s' LIMIT 1",
        NombreJugador[playerid]
    );

    ResultCache = mysql_query(Database, DB_Query);

    if (cache_num_rows(ResultCache)) {
        // Existe.
    } else {
        // No Existe.
    }

    cache_delete(ResultCache);
    return 1;
}


public OnPlayerCommandText(playerid, cmdtext[])
{
    // Código a ejecutar si el comando no coincide con "/yadayada".
    return 0; // Devuelve 0 para indicar que el comando no fue manejado.
}

public OnPlayerSpawn(playerid)
{
    SetPlayerPos(playerid, 1717.63, -1880.03, 16.1406);
    SetPlayerSkin(playerid, 240);
    SetPlayerHealth(playerid, 100);
    SetPlayerArmour(playerid, 100);
	return 1;
}

public OnPlayerDeath(playerid, killerid, reason)
{
   	return 1;
}

public OnPlayerRequestClass(playerid, classid)
{
	return 1;
}

public OnGameModeInit()
{
	SetGameModeText("Roleplay");
	ShowPlayerMarkers(1);
	ShowNameTags(1);
	AllowAdminTeleport(1);
	// MYSQL
	Database = mysql_connect("MYSQL_HOST, MYSQL USER, MYSQL_PASSWORD, MYSQL_BASE_DE_DATOS);
	if(Database == MYSQL_INVALID_HANDLE || Mysql_errno(Database) != 0){
		 print("MySQL: La conexion no se ha podido dar, se cierra el servido.");
		 SendRconCommand("exit");
		 return 1;
   }
	print("MySQL: La conexion ha sido establecida, exitosa!")
	return 1;
}

