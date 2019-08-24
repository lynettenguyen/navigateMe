### interactions ###

import json
import urllib.parse
import urllib.request

MAPQUEST_API_KEY = 'sgzaPT8T90u9qCnMsfGqkuHQ20WUPWuv'

BASE_MAPQUEST_URL = 'http://open.mapquestapi.com/directions/v2'
ELEVATION_BASE_URL ='http://open.mapquestapi.com/elevation/v1'


def build_search_url(destinations: ['locations']) -> str:
    '''With a given list of destinations, build a url'''
    complete_search_parameter = []
    complete_search_parameter.append(('key', MAPQUEST_API_KEY))
    for x in range(len(destinations)):
        if x == 0:
            from_parameter = ('from', destinations[0].replace(' ', ''))
            complete_search_parameter.append(from_parameter)
        else:
            to_parameter = ('to', destinations[x])
            complete_search_parameter.append(to_parameter)

    return BASE_MAPQUEST_URL + '/route?' + urllib.parse.urlencode(complete_search_parameter)

def build_elevation_url(lat_and_long: str) -> str:
    '''Using a str of lat and long, build a url to find the elevation of specified destinations'''
    search_parameters = [ ('key', MAPQUEST_API_KEY), ('unit', 'f')]
    end_of_search = '&latLngCollection=' + lat_and_long

    return ELEVATION_BASE_URL + '/profile?' + urllib.parse.urlencode(search_parameters) + end_of_search 


def get_result(url: str) -> dict:
    '''Gets the results from the URL in JSON'''
    response = None
    try:
        response = urllib.request.urlopen(url)
        json_text = response.read().decode(encoding = 'utf-8')
        return json.loads(json_text)
    finally:
        if response != None:
            response.close()

