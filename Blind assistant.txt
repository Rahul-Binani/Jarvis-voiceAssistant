package com.voicerecog.test;

//import java.io.*;
import java.io.IOException;
import java.text.SimpleDateFormat;

import com.sun.speech.freetts.*;

import java.time.format.DateTimeFormatter;
import java.time.LocalDate;

import java.util.*;
import java.time.LocalTime;

import edu.cmu.sphinx.api.Configuration;
import edu.cmu.sphinx.api.LiveSpeechRecognizer;
import edu.cmu.sphinx.api.SpeechResult;
import com.email.durgesh.Email;

public class VoiceRecognizer {


	public static void main(String[] args) throws IOException {
		Configuration configuration = new Configuration();		//configuration class under sphinx4 library
		
		configuration.setAcousticModelPath("resource:/edu/cmu/sphinx/models/en-us/en-us");
		//representation of sound
		configuration.setDictionaryPath("/Users/Rahul Binani/Desktop/JAVA/Voice assistant/src/com/voicerecog/resources/7472.dic");
		
		configuration.setLanguageModelPath("/Users/Rahul Binani/Desktop/JAVA/Voice assistant/src/com/voicerecog/resources/7472.lm");
		//2 methods which allow computer to understand what we speak
		//Tells computer to where to take input from
		
		LiveSpeechRecognizer recognize = new LiveSpeechRecognizer(configuration);
		//Listens in real time
		//use microphone io
		
		recognize.startRecognition(true);
		
		SpeechResult speechResult;

		final String VOICENAME = "kevin16";
		Voice voice;
		VoiceManager vm = VoiceManager.getInstance();
		voice = vm.getVoice(VOICENAME);
		
		
		voice.allocate();
		
		try
		{
		voice.speak("Hello there! How are you? How may I help You?");	
		}
		catch(Exception e)
		{
			
		}
		
		DateTimeFormatter dtfd = DateTimeFormatter.ofPattern("dd/MM/yyyy");
		DateTimeFormatter dtft = DateTimeFormatter.ofPattern("HH:mm:ss"); 
		
		LocalDate nowd = LocalDate.now();
		LocalTime nowt = LocalTime.now();
		
		
		   
		   Calendar calendar = Calendar.getInstance();
		   Date date = calendar.getTime();
		
		
		
		while((speechResult = recognize.getResult()) != null)		//Command recvd.
		{
			String command = speechResult.getHypothesis();			//returns command recvd.
			System.out.println("The input command is : " + command);
			
			if(command.equalsIgnoreCase("Open Chrome"))
				{
				Runtime.getRuntime().exec("cmd.exe /c start chrome");
				
				voice.allocate();
				try
				{
				voice.speak("Opening Chrome");	
				}
				catch(Exception e)
				{
					
				}
				}
				
			
			if(command.equalsIgnoreCase("Open Mail"))
			{
				Runtime.getRuntime().exec("cmd.exe /c start chrome www.gmail.com");
				voice.allocate();
				try
				{
				voice.speak("Opening Your E-mail");	
				}
				catch(Exception e)
				{
					
				}
			}
			if(command.equalsIgnoreCase("Open YouTube"))
			{
				Runtime.getRuntime().exec("cmd.exe /c start chrome www.youtube.com");
			voice.allocate();
			try
			{
			voice.speak("Opening YouTube for you");	
			}
			catch(Exception e)
			{
				
			}
			}
			
			else if (command.equalsIgnoreCase("Open Mozilla"))
			{
				Runtime.getRuntime().exec("cmd.exe /c start firefox");
				voice.allocate();
				try
				{
				voice.speak("Opening Mozilla Firefox");	
				}
				catch(Exception e)
				{
					
				}
			}
			
			else if (command.equalsIgnoreCase("Open Excel"))
			{
				Runtime.getRuntime().exec("cmd.exe /c start excel.exe");
				voice.allocate();
				try
				{
				voice.speak("Opening Excel spreadsheets");	
				}
				catch(Exception e)
				{
					
				}
			}
			
			else if (command.equalsIgnoreCase("Open outlook"))
			{
				Runtime.getRuntime().exec("cmd.exe /c start outlook.exe");
				voice.allocate();
				try
				{
				voice.speak("Opening Outlook");	
				}
				catch(Exception e)
				{
					
				}
			}
			
			else if (command.equalsIgnoreCase("Open editor"))
			{
				Runtime.getRuntime().exec("cmd.exe /c start eclipse.exe");
				voice.allocate();
				try
				{
				voice.speak("Opening Editor");	
				}
				catch(Exception e)
				{
					
				}
			}
			
			else if (command.equalsIgnoreCase("Play music"))
			{
				Runtime.getRuntime().exec("cmd.exe /c start chrome https://www.youtube.com/watch?v=ag1XtF_DDCI");
				voice.allocate();
				try
				{
				voice.speak("Playing music in YouTube");	
				}
				catch(Exception e)
				{
					
				}
			}
			
			else if (command.equalsIgnoreCase("Date today"))
			{
				voice.allocate();
				try
				{
				voice.speak(dtfd.format(nowd));
				}
				catch(Exception e)
				{
					
				}
			}
			
			else if (command.equalsIgnoreCase("Time now"))
			{
				voice.allocate();
				try
				{
				voice.speak(dtft.format(nowt));
				}
				catch(Exception e)
				{
					
				}
			}
			
			else if (command.equalsIgnoreCase("Din"))
			{
				voice.allocate();
				try
				{
				voice.speak(new SimpleDateFormat("EEEE", Locale.ENGLISH).format(date.getTime()));
				}
				catch(Exception e)
				{
					
				}
			}
						
			
			else if (command.equalsIgnoreCase("Sleep now"))
			{
				
				voice.allocate();
				try
				{
				voice.speak("Thank You for using me. Have a good day.");	
				}
				catch(Exception e)
				{
					
				}
				
				Runtime.getRuntime().exit(0);
			}
			
			//before trying to send an email, make sure the mail id you are using has a SWITCHED ON access on Less-Secure Apps.
			else if (command.equalsIgnoreCase("Send email"))
			{
			try {
				
				Email email = new Email("XYZ@gmail.com","yourPassword");	//Enter your mail id and password through which you want to send the email.
				
				//from
				email.setFrom("sender'sMailId","Name_with_which_you_want_to_send");
				
				email.setSubject("Just A Trial");	//subject
				
				email.setContent("<h1> This is the content. I hope it reaches you.</h1>", "text/html");			//content and content-type
				
				email.addRecipient("Recipient'sMailId");
				
				
				
				email.send();
				
			}
			catch(Exception e)
			{
				e.printStackTrace();
			}
			voice.allocate();
			try
			{
			voice.speak("Mail sent. Opening your gmail account now.");	
			}
			catch(Exception e)
			{
				
			}
			Runtime.getRuntime().exec("cmd.exe /c start chrome www.gmail.com");
			}
			
		}		
		}
	}
