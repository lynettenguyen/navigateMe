import urllib.request
import mapquest_interactions
import mapquest_output

def main_program() -> None:
    '''This program allows a user to input a list of locations and commands
       and will print out results from Mapquest'''
    try:
        locations_list = location_input()
        commands_list = user_commands()

        json_dict = get_json_dict(locations_list)

        
        if valid_route(json_dict):
            print()
            run_command_list = mapquest_output.output_commands(commands_list)
            mapquest_output.run_command(run_command_list, json_dict)

            print('Directions Courtesy of MapQuest; Map Data Copyright OpenStreetMap Contributors')

        else:
            print('NO ROUTE FOUND')

    except urllib.error.URLError:
        print()
        print('MAPQUEST ERROR')

    
    
def location_input() -> list:
    '''The user tells the program how many destinations they want and
       then types each location into the program'''
    location_list = []
    num = int(input())
    if num <= 1:
        print('ERROR')
        location_input()
    else:
        for x in range(num):
            location = str(input())
            location_list.append(location)
    return location_list
        
def get_json_dict(locations: list) -> dict:
    '''Gets the Mapquest API for the desired destinations'''
    url = mapquest_interactions.build_search_url(locations)

    return mapquest_interactions.get_result(url)

def valid_route(json_dict: dict) -> bool:
    '''Checks if there is a valid route with the specific locations'''
    if json_dict['info']['messages'] == ['We are unable to route with the given locations.']:
        return False
    else:
        return True

def user_commands() -> list:
    '''The user tells the program how many commands they would like to run
       and types in which commands'''
    command_list = []
    num = int(input())
    if num < 1:
        print('ERROR')
        user_commands()
    else:
        for x in range(num):
            command = str(input())
            command_list.append(command)
    return command_list 

if __name__ == '__main__':
    main_program()
