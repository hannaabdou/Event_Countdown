import 'package:flutter/material.dart';
import 'package:intl/intl.dart';
import 'dart:async';

void main() {
  runApp(EventCountdownApp());
}

class EventCountdownApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Event Countdown',
      theme: ThemeData(
        brightness: Brightness.light,
        primarySwatch: Colors.teal,
        scaffoldBackgroundColor: Colors.white,
        textTheme: TextTheme(
          bodyText1: TextStyle(color: Colors.black87, fontFamily: 'Poppins'),
          bodyText2: TextStyle(color: Colors.black54, fontFamily: 'Poppins'),
        ),
      ),
      home: EventHomePage(),
    );
  }
}

class EventHomePage extends StatefulWidget {
  @override
  _EventHomePageState createState() => _EventHomePageState();
}

class _EventHomePageState extends State<EventHomePage> {
  final List<Map<String, dynamic>> _events = [];
  Timer? _timer;

  @override
  void initState() {
    super.initState();
    _startTimer();
  }

  @override
  void dispose() {
    _timer?.cancel();
    super.dispose();
  }

  void _startTimer() {
    _timer = Timer.periodic(Duration(seconds: 1), (timer) {
      setState(() {}); // Refresh the UI every second
    });
  }

  void _addEvent(String eventName, DateTime eventDate) {
    setState(() {
      _events.add({
        'name': eventName,
        'date': eventDate,
      });
    });
  }

  void _editEvent(int index, String eventName, DateTime eventDate) {
    setState(() {
      _events[index] = {
        'name': eventName,
        'date': eventDate,
      };
    });
  }

  void _deleteEvent(int index) {
    setState(() {
      _events.removeAt(index);
    });
  }

  String _getCountdown(DateTime eventDate) {
    final Duration difference = eventDate.difference(DateTime.now());
    if (difference.isNegative) {
      return 'Event passed';
    }
    final days = difference.inDays;
    final hours = difference.inHours.remainder(24);
    final minutes = difference.inMinutes.remainder(60);
    final seconds = difference.inSeconds.remainder(60);
    return '$days days, $hours hours, $minutes minutes, $seconds seconds';
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Event Countdown', style: TextStyle(fontFamily: 'Poppins')),
        backgroundColor: Colors.teal,
        elevation: 0,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            Expanded(
              child: _events.isEmpty
                  ? Center(
                      child: Text(
                        'No events yet!',
                        style: TextStyle(fontSize: 18, color: Colors.grey),
                      ),
                    )
                  : ListView.builder(
                      itemCount: _events.length,
                      itemBuilder: (context, index) {
                        final event = _events[index];
                        return EventCard(
                          eventName: event['name'],
                          eventDate: event['date'],
                          countdown: _getCountdown(event['date']),
                          onEdit: () {
                            _showEditEventDialog(index, event['name'], event['date']);
                          },
                          onDelete: () {
                            _deleteEvent(index);
                          },
                        );
                      },
                    ),
            ),
            Padding(
  padding: const EdgeInsets.all(10.0),
  child: ElevatedButton(
    style: ElevatedButton.styleFrom(
      primary: Colors.teal, // Background color
      onPrimary: Colors.white, // Text color
      padding: EdgeInsets.symmetric(vertical: 15, horizontal: 30), // Add horizontal padding
      shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.circular(30), // Rounded rectangle shape
      ),
      elevation: 6, // Adding a more prominent shadow
      shadowColor: Colors.tealAccent.withOpacity(0.5), // Shadow color
    ),
    onPressed: () {
      _showAddEventDialog();
    },
    child: Text('Add Event', style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold)), // Adjusted text size and weight
  ),
),
          ],
        ),
      ),
    );
  }

  void _showAddEventDialog() {
    String eventName = '';
    DateTime selectedDate = DateTime.now();

    showDialog(
      context: context,
      builder: (context) {
        return AlertDialog(
          backgroundColor: Colors.white,
          title: Text('Add New Event', style: TextStyle(color: Colors.black)),
          content: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              TextField(
                style: TextStyle(color: Colors.black),
                decoration: InputDecoration(
                  labelText: 'Event Name',
                  labelStyle: TextStyle(color: Colors.grey),
                  border: OutlineInputBorder(),
                ),
                onChanged: (value) {
                  eventName = value;
                },
              ),
              SizedBox(height: 10),
              ElevatedButton(
                style: ElevatedButton.styleFrom(primary: Colors.teal),
                onPressed: () async {
                  final DateTime? picked = await showDatePicker(
                    context: context,
                    initialDate: selectedDate,
                    firstDate: DateTime.now(),
                    lastDate: DateTime(2101),
                  );
                  if (picked != null && picked != selectedDate) {
                    setState(() {
                      selectedDate = picked;
                    });
                  }
                },
                child: Text('Select Date', style: TextStyle(color: Colors.white)),
              ),
            ],
          ),
          actions: [
            ElevatedButton(
              onPressed: () {
                if (eventName.isNotEmpty) {
                  _addEvent(eventName, selectedDate);
                }
                Navigator.of(context).pop();
              },
              style: ElevatedButton.styleFrom(primary: Colors.teal),
              child: Text('Add', style: TextStyle(color: Colors.white)),
            ),
          ],
        );
      },
    );
  }

  void _showEditEventDialog(int index, String eventName, DateTime eventDate) {
    String updatedName = eventName;
    DateTime selectedDate = eventDate;

    showDialog(
      context: context,
      builder: (context) {
        return AlertDialog(
          backgroundColor: Colors.white,
          title: Text('Edit Event', style: TextStyle(color: Colors.black)),
          content: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              TextField(
                controller: TextEditingController(text: eventName),
                style: TextStyle(color: Colors.black),
                decoration: InputDecoration(
                  labelText: 'Event Name',
                  labelStyle: TextStyle(color: Colors.grey),
                  border: OutlineInputBorder(),
                ),
                onChanged: (value) {
                  updatedName = value;
                },
              ),
              SizedBox(height: 10),
              ElevatedButton(
                style: ElevatedButton.styleFrom(primary: Colors.teal),
                onPressed: () async {
                  final DateTime? picked = await showDatePicker(
                    context: context,
                    initialDate: selectedDate,
                    firstDate: DateTime.now(),
                    lastDate: DateTime(2101),
                  );
                  if (picked != null && picked != selectedDate) {
                    setState(() {
                      selectedDate = picked;
                    });
                  }
                },
                child: Text('Select Date', style: TextStyle(color: Colors.white)),
              ),
            ],
          ),
          actions: [
            ElevatedButton(
              onPressed: () {
                if (updatedName.isNotEmpty) {
                  _editEvent(index, updatedName, selectedDate);
                }
                Navigator.of(context).pop();
              },
              style: ElevatedButton.styleFrom(primary: Colors.teal),
              child: Text('Update', style: TextStyle(color: Colors.white)),
            ),
          ],
        );
      },
    );
  }
}

class EventCard extends StatelessWidget {
  final String eventName;
  final DateTime eventDate;
  final String countdown;
  final VoidCallback onEdit;
  final VoidCallback onDelete;

  const EventCard({
    Key? key,
    required this.eventName,
    required this.eventDate,
    required this.countdown,
    required this.onEdit,
    required this.onDelete,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 8,
      shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.circular(15),
      ),
      margin: EdgeInsets.symmetric(vertical: 10),
      child: Container(
        decoration: BoxDecoration(
          gradient: LinearGradient(
            colors: [Colors.teal.shade300, Colors.teal.shade500],
            begin: Alignment.topLeft,
            end: Alignment.bottomRight,
          ),
          borderRadius: BorderRadius.circular(15),
        ),
        padding: EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              eventName,
              style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold, color: Colors.white, fontFamily: 'Poppins'),
            ),
            SizedBox(height: 6),
            Text(
              countdown,
              style: TextStyle(fontSize: 18, color: Colors.white70, fontFamily: 'Poppins'),
            ),
            SizedBox(height: 10),
            Text(
              'Event Date: ${DateFormat('yyyy-MM-dd').format(eventDate)}',
              style: TextStyle(fontSize: 14, color: Colors.white70, fontFamily: 'Poppins'),
            ),
            SizedBox(height: 10),
            Row(
              mainAxisAlignment: MainAxisAlignment.end,
              children: [
                ElevatedButton(
                  onPressed: onEdit,
                  style: ElevatedButton.styleFrom(
                    primary: Colors.white, // Background color
                    onPrimary: Colors.teal, // Text color
                    shape: RoundedRectangleBorder(
                      borderRadius: BorderRadius.circular(20), // Rounded corners
                    ),
                    padding: EdgeInsets.symmetric(horizontal: 10, vertical: 8),
                  ),
                  child: Row(
                    children: [
                      Icon(Icons.edit, color: Colors.teal),
                      SizedBox(width: 5),
                      Text('Edit', style: TextStyle(fontSize: 14)),
                    ],
                  ),
                ),
                SizedBox(width: 10),
                ElevatedButton(
                  onPressed: onDelete,
                  style: ElevatedButton.styleFrom(
                    primary: Colors.red, // Background color
                    onPrimary: Colors.white, // Text color
                    shape: RoundedRectangleBorder(
                      borderRadius: BorderRadius.circular(20), // Rounded corners
                    ),
                    padding: EdgeInsets.symmetric(horizontal: 10, vertical: 8),
                  ),
                  child: Row(
                    children: [
                      Icon(Icons.delete, color: Colors.white),
                      SizedBox(width: 5),
                      Text('Delete', style: TextStyle(fontSize: 14)),
                    ],
                  ),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
