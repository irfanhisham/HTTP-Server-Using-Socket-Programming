import socket

from http.server import HTTPServer, BaseHTTPRequestHandler

''' 

This main function is for to define the port for server
and also create a socket

'''
def main():
    
    PORT = 8000
    server_address = ('localhost', PORT)
    server = HTTPServer(server_address, requestHandler)
    serversocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    print ('Server running on port %s' % PORT)
    server.serve_forever()
    serversocket.listen(1) 

    
'''

From line 32 to line 108

A client makes connection request to the server.
The server sends a response to the client telling the client how to proceed.
The client can view resources if he/she wishes.

'''

class requestHandler(BaseHTTPRequestHandler):

    def do_GET(self):
        if self.path.endswith('/Client'):
            self.send_response(200)
            self.send_header('content-type', 'text/html')
            self.end_headers()
        
            output = ''
            output += '<html><body>'
            output += '<h1>Assignment EKT434 HTTP Server</h1>'
            output += '<h2>Do you want to continue? Yes or No</h2>'
            output += '<h3><a href="/Client/Yes">Yes</a></h3>'
            output += '<h3><a href="/Client/No">No</a></h3>'
            output += '</br>'
            output += '<body><html>'
            self.wfile.write(output.encode())
            
        
        if self.path.endswith('/Yes'):
            self.send_response(200)
            self.send_header('content-type', 'text/html')
            self.end_headers()
            
            output = ''
            output += '<html><body>'
            output += '<h1>Assignment EKT434 HTTP Server</h1>'
            output += '<h3><a href="/Client/Yes/ViewPage">1. View Page</a></h3>'
            output += '<h3><a href="/Client/Yes">2. Exit</a></h3>'
            output += '</br>'
            output += '<body><html>'
            self.wfile.write(output.encode())
                       
       
        if self.path.endswith('/ViewPage'):
            self.send_response(200)
            self.send_header('content-type', 'text/html')
            self.end_headers()
        
            output = ''
            output += '<html><body>'
            output += '<h1>Assignment EKT434 HTTP Server</h1>'
            output += '<h2>After Viewing Page</h2>'
            output += '<h2>Do you want to continue? Yes or No</h2>'
            output += '<h3><a href="/Client/Yes/ViewPage/Yes(AfterViewingPage)">Yes</a></h3>'
            output += '<h3><a href="/Client/Yes/ViewPage/">No</a></h3>'
            output += '</br>'
            output += '<body><html>'
            self.wfile.write(output.encode())  
            

        if self.path.endswith('/Yes(AfterViewingPage)'):
            self.send_response(200)
            self.send_header('content-type', 'text/html')
            self.end_headers()
        
            output = ''
            output += '<html><body>'
            output += '<h1>Assignment EKT434 HTTP Server</h1>'
            output += '<h3><a href="/Client/Yes/ViewPage/Yes(AfterViewingPage)">1. View Page</a></h3>'
            output += '<h3><a href="/Client/Yes/ViewPage/Yes(AfterViewingPage)/Exit">2. Exit</a></h3>'
            output += '</br>'
            output += '<body><html>'
            self.wfile.write(output.encode())              
                       
   
        if self.path.endswith('/Exit'):
            self.send_response(200)
            self.send_header('content-type', 'text/html')
            self.end_headers()
        
            output = ''
            output += '<html><body>'
            output += '<h1>Assignment EKT434 HTTP Server</h1>'
            output += '<h3><a href="/Client/Yes/ViewPage/Yes(AfterViewingPage)/Exit">Bye</a></h3>'
            output += '<body><html>'
            self.wfile.write(output.encode())
            
            
'''

To execute code only if the file was run directly, and not imported.

''' 

if __name__ == '__main__':
    main()
