#include <iostream>

const int NIMOTSU_COUNT = 2;
const int MAP_ROWS_COUNT = 9;
const int MAP_COLS_COUNT = 5;

static int nimotsupos[NIMOTSU_COUNT][2];
static int goalpos[NIMOTSU_COUNT][2];

static char map[MAP_COLS_COUNT][MAP_ROWS_COUNT];
static char inputValue;

static int playerPosX;
static int playerPosY;

static int prevX = playerPosX;
static int prevY = playerPosY;

static int nimotsuX = 0;
static int nimotsuY = 0;

enum class EDirection : short
{
	UP = 0,
	DOWN,
	LEFT,
	RIGHT,
};

enum class ETileType : short
{
	WALL = 0,
	NORMAL,
	GOAL,
	NIMOTSU,
};

static short isClear;
static short isMovable;
static EDirection direction;
static ETileType moveMapType;
static ETileType prevTileType;

void draw();

using namespace std;

void Init( void )
{
	memset( nimotsupos, 0, sizeof( int ) * NIMOTSU_COUNT );
	memset( goalpos, 0, sizeof( int ) * NIMOTSU_COUNT );
	memset( map, 0, sizeof( char ) * (MAP_COLS_COUNT * MAP_ROWS_COUNT) );
	
	inputValue = 0;

	prevX = 0;
	prevY = 0;

	playerPosX = 0;
	playerPosY = 0;

	prevTileType = ETileType::NORMAL;
	moveMapType = ETileType::NORMAL;

	strcpy( map[0], "########" );
	strcpy( map[1], "# .. p #" );
	strcpy( map[2], "# oo   #" );
	strcpy( map[3], "#      #" );
	strcpy( map[4], "########" );

	nimotsupos[0][0] = 2;
	nimotsupos[0][1] = 2;

	nimotsupos[1][0] = 2;
	nimotsupos[1][1] = 3;

	goalpos[0][0] = 1;
	goalpos[0][1] = 2;

	goalpos[1][0] = 1;
	goalpos[1][1] = 3;
}

bool IsNextWall( void )
{
	bool flag = false;
	switch( direction )
	{
		case EDirection::UP:
			flag = map[(playerPosX - 1)][playerPosY] == '#' ? true : false;
			break;
		case EDirection::DOWN:
			flag = map[(playerPosX + 1)][playerPosY] == '#' ? true : false;
			break;
		case EDirection::LEFT:
			flag = map[playerPosX][(playerPosY - 1)] == '#' ? true : false;
			break;
		case EDirection::RIGHT:
			flag = map[playerPosX][(playerPosY + 1)] == '#' ? true : false;
			break;
		default:
			return false;
	}

	return flag;
}


bool IsGoalNextWall( void )
{
	bool flag = false;
	switch( direction )
	{
		case EDirection::UP:
			flag = map[(playerPosX - 1)][playerPosY] == '#' ? true : false;
			break;
		case EDirection::DOWN:
			flag = map[(playerPosX + 1)][playerPosY] == '#' ? true : false;
			break;
		case EDirection::LEFT:
			flag = map[playerPosX][(playerPosY - 1)] == '#' ? true : false;
			break;
		case EDirection::RIGHT:
			flag = map[playerPosX][(playerPosY + 1)] == '#' ? true : false;
			break;
		default:
			return false;
	}

	return flag;
}


bool IsNextGoal( void )
{
	bool flag = false;
	switch( direction )
	{
		case EDirection::UP:
			flag = map[(playerPosX - 1)][playerPosY] == '.' ? true : false;
			break;
		case EDirection::DOWN:
			flag = map[(playerPosX + 1)][playerPosY] == '.' ? true : false;
			break;
		case EDirection::LEFT:
			flag = map[playerPosX][(playerPosY - 1)] == '.' ? true : false;
			break;
		case EDirection::RIGHT:
			flag = map[playerPosX][(playerPosY + 1)] == '.' ? true : false;
			break;
		default:
			return false;
	}

	if( true == flag )
	{
		moveMapType = ETileType::GOAL;
	}

	return flag;
}

bool IsNextNimotsu( void )
{
	bool flag = false;
	switch( direction )
	{
		case EDirection::UP:
			flag = map[(playerPosX - 1)][playerPosY] == 'o' ? true : false;
			break;
		case EDirection::DOWN:
			flag = map[(playerPosX + 1)][playerPosY] == 'o' ? true : false;
			break;
		case EDirection::LEFT:
			flag = map[playerPosX][(playerPosY - 1)] == 'o' ? true : false;
			break;
		case EDirection::RIGHT:
			flag = map[playerPosX][(playerPosY + 1)] == 'o' ? true : false;
			break;
		default:
			return false;
	}

	if( true == flag )
	{
		moveMapType = ETileType::GOAL;
	}

	return flag;
}

bool IsCanPush( void )
{
	bool flag = false;
	switch( direction )
	{
		case EDirection::UP:
			flag = map[(playerPosX - 1)][playerPosY] == 'o' ? true : false;
			break;
		case EDirection::DOWN:
			flag = map[(playerPosX + 1)][playerPosY] == 'o' ? true : false;
			break;
		case EDirection::LEFT:
			flag = map[playerPosX][(playerPosY - 1)] == 'o' ? true : false;
			break;
		case EDirection::RIGHT:
			flag = map[playerPosX][(playerPosY + 1)] == 'o' ? true : false;
			break;
		default:
			return false;
	}

	if( true == flag )
	{
		switch( direction )
		{
			case EDirection::UP:
				flag = map[(playerPosX - 2)][playerPosY] == 'o' ? false : true;
				break;
			case EDirection::DOWN:
				flag = map[(playerPosX + 2)][playerPosY] == 'o' ? false : true;
				break;
			case EDirection::LEFT:
				flag = map[playerPosX][(playerPosY - 2)] == 'o' ? false : true;
				break;
			case EDirection::RIGHT:
				flag = map[playerPosX][(playerPosY + 2)] == 'o' ? false : true;
				break;
			default:
				return false;
		}
	}

	if( true == flag )
	{
		switch( direction )
		{
			case EDirection::UP:
				flag = map[(playerPosX - 2)][playerPosY] == '#' ? false : true;
				break;
			case EDirection::DOWN:
				flag = map[(playerPosX + 2)][playerPosY] == '#' ? false : true;
				break;
			case EDirection::LEFT:
				flag = map[playerPosX][(playerPosY - 2)] == '#' ? false : true;
				break;
			case EDirection::RIGHT:
				flag = map[playerPosX][(playerPosY + 2)] == '#' ? false : true;
				break;
			default:
				return false;
		}
	}

	return flag;
}

void MoveUp( void )
{
	playerPosX -= 1;
}

void MoveDown( void )
{
	playerPosX += 1;
}

void MoveLeft( void )
{
	playerPosY -= 1;
}

void MoveRight( void )
{
	playerPosY += 1;
}

void UpdateNimotsuPos( void )
{
	switch( direction )
	{
		case EDirection::UP:
			if( nimotsupos[0][0] == (playerPosX) && nimotsupos[0][1] == playerPosY )
			{
				nimotsupos[0][0] = playerPosX - 1;
			}
			else if( nimotsupos[1][0] == (playerPosX) && nimotsupos[1][1] == playerPosY )
			{
				nimotsupos[1][0] = playerPosX - 1;
			}
			break;
		case EDirection::DOWN:
			if( nimotsupos[0][0] == (playerPosX) && nimotsupos[0][1] == playerPosY )
			{
				nimotsupos[0][0] = playerPosX + 1;
			}
			else if( nimotsupos[1][0] == (playerPosX) && nimotsupos[1][1] == playerPosY )
			{
				nimotsupos[1][0] = playerPosX + 1;
			}
			break;
		case EDirection::LEFT:
			if( nimotsupos[0][0] == playerPosX && nimotsupos[0][1] == playerPosY )
			{
				nimotsupos[0][1] = playerPosY - 1;
			}
			else if( nimotsupos[1][0] == playerPosX && nimotsupos[1][1] == playerPosY )
			{
				nimotsupos[1][1] = playerPosY - 1;
			}
			break;
		case EDirection::RIGHT:
			if( nimotsupos[0][0] == playerPosX && nimotsupos[0][1] == playerPosY )
			{
				nimotsupos[0][1] = playerPosY + 1;
			}
			else if( nimotsupos[1][0] == playerPosX && nimotsupos[1][1] == playerPosY )
			{
				nimotsupos[1][1] = playerPosY + 1;
			}
	}
}

void PushUp( void )
{
	nimotsuX = playerPosX - 2;
	nimotsuY = playerPosY;
	
	MoveUp();
	UpdateNimotsuPos();
}

void PushDown( void )
{
	nimotsuX = playerPosX + 2;
	nimotsuY = playerPosY;

	MoveDown();
	UpdateNimotsuPos();
}

void PushLeft( void )
{
	nimotsuX = playerPosX;
	nimotsuY = playerPosY - 2;

	MoveLeft();
	UpdateNimotsuPos();
}

void PushRight( void )
{
	nimotsuX = playerPosX;
	nimotsuY = playerPosY + 2;

	MoveRight();
	UpdateNimotsuPos();
}

ETileType GetCurTileType( void )
{
	if( goalpos[0][0] == playerPosX && goalpos[0][1] == playerPosY ||
		goalpos[1][0] == playerPosX && goalpos[1][1] == playerPosY )
	{
		return ETileType::GOAL;
	}
	else
	{
		return ETileType::NORMAL;
	}
}

void getInput()
{
	cin >> inputValue;
	switch( inputValue )
	{
		case 'w':
		case 'W':
			direction = EDirection::UP;
			break;
		case 's':
		case 'S':
			direction = EDirection::DOWN;
			break;
		case 'a':
		case 'A':
			direction = EDirection::LEFT;
			break;
		case 'd':
		case 'D':
			direction = EDirection::RIGHT;
			break;
		case 'q':
		case 'Q':
			return;
		case 'r':
		case 'R':
			Init();
			draw();
			break;
	}

	return;
}

bool IsClear( void )
{
	if( (goalpos[0][0] == nimotsupos[0][0] && goalpos[0][1] == nimotsupos[0][1]) &&
		(goalpos[1][0] == nimotsupos[1][0] && goalpos[1][1] == nimotsupos[1][1]) )
	{
		return true;
	}

	return false;
}

void updateGame()
{
	if( false == IsClear() )
	{
		if( true == IsCanPush() )
		{
			prevX = playerPosX;
			prevY = playerPosY;

			map[prevX][prevY] = ' ';

			switch( direction )
			{
				case EDirection::UP:
					PushUp();
					break;
				case EDirection::DOWN:
					PushDown();
					break;
				case EDirection::LEFT:
					PushLeft();
					break;
				case EDirection::RIGHT:
					PushRight();
					break;
			}

			map[playerPosX][playerPosY] = 'p';
			map[nimotsuX][nimotsuY] = 'o';

			prevTileType = GetCurTileType();
		}
		else
		{
			isMovable = 0;

			if( false == IsNextNimotsu() &&
				(false == IsNextWall() || true == IsNextGoal()) )
			{
				isMovable = 1;
			}

			if( 1 == isMovable )
			{
				prevX = playerPosX;
				prevY = playerPosY;

				if( ETileType::NORMAL == prevTileType )
				{
					map[prevX][prevY] = ' ';
				}
				else if( ETileType::GOAL == prevTileType )
				{
					map[prevX][prevY] = '.';
				}

				switch( direction )
				{
					case EDirection::UP:
						MoveUp();
						break;
					case EDirection::DOWN:
						MoveDown();
						break;
					case EDirection::LEFT:
						MoveLeft();
						break;
					case EDirection::RIGHT:
						MoveRight();
						break;
				}

				map[playerPosX][playerPosY] = 'p';

				prevTileType = GetCurTileType();
			}
		}

		if( true == IsClear() )
		{
			cout << "clear!!" << endl;
		}
	}
}

void draw()
{
	for( auto i = 0; i < MAP_COLS_COUNT; ++i )
	{
		cout << map[i] << endl;
	}

	return;
}

int main( void )
{
	Init();
	
	playerPosX = 1;
	playerPosY = 5;

	draw();

	while( true )
	{
		getInput();
		updateGame();
		draw();
	}

	return 0;
}
