### output ###

import mapquest_interactions

class Directions:
    '''Prints the direction and steps to the specified locations'''
    def output(self, json_dict: dict) -> None:
        print('DIRECTIONS')
        for object in json_dict['route']['legs']:
            for steps in object['maneuvers']:
                print(steps['narrative'])
        print()

class LatLong:
    '''Prints out the LatLongs of each location specified'''
    def output(self, json_dict: dict) -> None:
        print('LATLONGS')
        for object in json_dict['route']['locations']:
            lat = object['latLng']['lat']
            lng = object['latLng']['lng']
            
            if lat >= 0:
                direction_lat = 'N'
            else:
                direction_lat = 'S'
            if lng >= 0:
                direction_lng = 'E'
            else:
                direction_lng = 'W'

            display = '{:.2f}{} {:.2f}{}'.format(abs(lat), direction_lat, abs(lng), direction_lng)

            print(display)
        print()

class Total_time:
    def output(self, json_dict: dict) -> None:
        '''Takes a dictionary in JSON text and returns the total time in minutes'''
        time = json_dict['route']['time'] / 60
        print('TOTAL TIME: ' + str(round(time)) + ' minutes')
        print()


class Total_distance:
    '''Prints out the total distance in miles'''
    def output(self, json_dict: dict) -> None:
        miles = json_dict['route']['distance']
        print('TOTAL DISTANCE: ' + str(round(miles)) + ' miles')
        print()

                            
class Elevation:
    '''Prints out the elevation in all specified locations'''
    def output(self, json_dict: dict) -> None:
        print('ELEVATIONS')
        lat_long_list = latlong_str(json_dict).split()
        for location in lat_long_list:
            elevation_dict = mapquest_interactions.get_result(mapquest_interactions.build_elevation_url(location))
            for object in elevation_dict['elevationProfile']:
                print(round(object['height']))
        print()

        
def latlong_str(json_dict: dict) -> list:
    '''Takes a dictionary in JSON text and puts LatLongs in a list'''
    lat_long_str = ''
    for object in json_dict['route']['locations']:
        lat_long_str += str(object['latLng']['lat']) +','
        lat_long_str += str(object['latLng']['lng']) + ','

        lat_long_str += ' '
        
    return lat_long_str[0:-1]


def output_commands(list_of_input: list) -> None:
    '''Takes a list of the user's input and runs the command'''
    run_command_list = []
    for command in list_of_input:
        if command == 'LATLONG':
            run_command_list.append(LatLong())
        elif command == 'STEPS':
            run_command_list.append(Directions())
        elif command == 'TOTALTIME':
            run_command_list.append(Total_time())
        elif command == 'TOTALDISTANCE':
            run_command_list.append(Total_distance())
        elif command == 'ELEVATION':
            run_command_list.append(Elevation())
    return run_command_list

def run_command(run_command_list: list, json_dict: dict) -> None:
    for command in run_command_list:
        command.output(json_dict)
