# DXF-Import
Python module that can read in a DXF file, extract basic geometric elements, and output a list of each element along with the coordinates of each element and any pertinent attributes.

Functions:

import_dxf_file(filename: str) -> List[Dict [str, List[Tuple[float,...]]]]

        Summary:
            Importing a DXF file and returning a list of entities

        Args:
            filename (str): DXF filename with path

        Raises:
            Exception: Passed file name is not found, corrupt, or not a DXF file
            Warning: Unknown Geometry is found

        Returns:
            List[Dict [str, List[tuple(float)]]]: A list of all geometry names followed by a unique ID # and a list of associated points in 2D/3D, represented in microns and degrees

            List of supported geometries and how they are stored
                LINE: ('LINE#': [START (X,Y,Z), END (X,Y,Z)])
                CIRCLE: ('CIRCLE#': [RADIUS (#), CENTER (X,Y,Z), PLANE (X,Y,Z)])
                ARC: ('ARC#': [RADIUS/START ANGLE/END ANGLE(#,#,#), CENTER (X,Y,Z), PLANE (X,Y,Z)])
                ELLIPSE: ('ELLIPSE#': [CENTER (X,Y,Z), LENGTH OF MAJOR AXIS (X,Y,Z), RATIO OF MINOR TO MAJOR AXIS (#)])
                SPLINE: ('SPLINE#': [DEGREE, CLOSED, # CONTROL POINTS (#,BOOLEAN,#), CONTROL POINT(S) (X,Y,Z), KNOTS (#,...), WEIGHTS (#,...)])
                LWPOLYLINE: ('LWPOLYLINE#:' POINT VALUES [X,Y,Z,START WIDTH,END WIDTH,BULGE], CLOSED/OPEN [BOOLEAN])

export_dxf_file(filename: str, scans: List[Dict [str, List[Tuple[float,...]]]], exportunits: str = "um") -> bool

        Summary:
            Exporting a DXF file from a list of entities

        Args:
            filename (str): DXF filename with path
            scans (List[Dict [str, List[Tuple[float,...]]]]): List of geometries to write to DXF file
            units (int, optional): [description]. Units to export DXF in, defaults 13=Microns.

        Raises:
            Exception: No scans are passed
            Exception: No file extension is passed
            Exception: Invalid units are passed
            Warning: Unknown Geometry is found

        Returns:
            bool: True upon successful completion

import_txt_file(filname: str, units: str = "um") -> List[Dict [str, List[Tuple[float,...]]]]

        Summary:
            Imports a list of points from a textfile

        Args:
            filname (str): TXT filename with path
            units (str, optional): Units to import TXT in, defaults to Microns.

        Raises:
            Exception: Passed file name is not found

        Returns:
            List[Dict [str, List[Tuple[float,...]]]]: A list of all geometry names followed by a unique ID # and a list of associated points in 2D/3D

import_csv_file(filename: str) -> List[Dict [str, List[Tuple[float,...]]]]

        TODO